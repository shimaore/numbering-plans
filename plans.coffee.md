Specified plans
---------------

    plans =
      1: require './plans/1'
      239: require './plans/239'
      262: require './plans/262'
      269: require './plans/269'
      33: require './plans/33'
      41: require './plans/41'
      508: require './plans/508'
      590: require './plans/590'
      594: require './plans/594'
      596: require './plans/596'
      62: require './plans/62'
      # 94: require './plans/94'

Yet-to-be-specified plans
-------------------------

    to_be_done = require './plans/to-be-done'

    for prefix, plan of to_be_done.plan
      do (prefix,plan) ->
        plans[prefix] ?=
          name: plan.name
          country: plan.country
          plan: {}
          # '': min:plan.min, max:plan.max, country: plan.country, name:plan.name

    plans[''] =
      name: 'Invalid country code'
      plan:
        '': block:true

    module.exports = plans
