Numbering plans
===============

Goals
-----

This project aims to build a list of international numbering plans for the purposes of:
- building dialing plans for customers, preventing to flag missing routes where the customer actually misdialed;
- helping to build LCR routing tables;
- helping to build rating tables.

It aims to be updated regularly to adapt to changes in international numbering plans. Contributions are welcome in the form of a Pull Request on [github](https://github.com/shimaore/numbering-plans)!

Validating numbers
------------------

    var numbers = require('numbering-plans')

    numbers.validate('12123141212')
    # returns:
    # { min: 10, max: 10, mixed: true, geographic: true, name: 'NY',
    #   country: 'us', conterminous: true, national_name: 'NANPA',
    #   full_name: 'NY (NANPA)' }

    numbers.validate('33612341234')
    # { max: 9, min: 9, mobile: true, country: 'fr',
    #   national_name: 'France', full_name: 'France' }

    numbers.validate('33_112')
    # { max: 3, min: 3, special: true, emergency: true,
    #   country: 'fr', national_name: 'France', full_name: 'France' }

    numbers.validate('3397234713')
    # false → number is invalid

    numbers.validate('4372617278')
    # null → unable to decide

Conventions
-----------

Available fields, where applicable, are:

- `min`: minimum length of _national_ number
- `max`: maximum lenght of _national_ number

One of:
- `block` -- non-dialable, non-routable, etc.
- `fixed`
- `mobile`
- 'mixed' -- could be fixed or mobile (e.g. NANPA)
- `special`
- `value_added`

For `mixed`:
- `geographic` might be true (e.g. US geographic numbers) or false (e.g. US non-geo)
- `corporate` might be true

For `fixed`:
- `geographic`
- `corporate`

For `value_added`:
- `freephone`
- `shared_cost`
- `personal`
- `premium`
- `adult`

For `special`:
- `voicemail`
- `test`
- `vpn`
- `emergency`

If a field is absent its value is assumed to be `false`.

Other fields might be available for specific destinations.

The numbering plans are established with the convention that national-only, short numbers, etc. are routed using `_` as a separator between the country-code and the national number.
