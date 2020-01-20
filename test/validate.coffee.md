    {expect} = chai = require 'chai'
    chai.should()

    describe 'validate', ->
      plans = require '..'

      it 'should reject missing numbers', ->
        plans.validate null
          .should.be.false

      it 'should accept non-geo FR numbers', ->
        a = plans.validate '33972342713'
        a.should.have.property 'fixed', true
        a.should.have.property 'geographic', false

      it 'should accept fixed geo FR numbers', ->
        a = plans.validate '33467891202'
        a.should.have.property 'fixed', true
        a.should.have.property 'geographic', true

      it 'should reject invalid FR numbers', ->
        plans.validate '3397234713'
          .should.be.false

      it 'should reject invalid FR numbers', ->
        plans.validate '33199001234'
          .should.be.false

      it 'should reject invalid FR numbers', ->
        plans.validate '33263781781'
          .should.be.false

      it 'should accept FR short numbers', ->
        plans.validate '33_112'
          .should.have.property 'emergency', true

      it 'should accept US numbers', ->
        plans.validate '12123141212'
          .should.have.property 'name', 'NY'

      it 'should reject unwanted US numbers', ->
        plans.validate '12125551212'
          .should.be.false
        plans.validate '11005551212'
          .should.be.false

      it 'should ignore numbers it does not know about', ->
        expect plans.validate '4472617278'
          .to.be.null
        expect plans.validate '881612345678'
          .to.be.null

      it 'should reject invalid country codes', ->
        expect plans.validate '978123456'
          .to.be.false

      it 'should reject unknown country codes', ->
        expect plans.validate '34963861234'
          .to.be.null

      it 'should accept E.164 numbers', ->
        a = plans.validate '+33972342713'
        a.should.have.property 'fixed', true
        a.should.have.property 'geographic', false

      it 'should accept BE numbers', ->
        a = plans.validate '+3264212345'
        a.should.have.property 'fixed', true
        a.should.have.property 'geographic', true
        a = plans.validate '+3264412345'
        a.should.have.property 'fixed', true
        a.should.have.property 'geographic', true
        a = plans.validate '+3247712345'
        a.should.have.property 'mobile', true

      it 'should accept RU numbers', ->
        a = plans.validate '+78692512345'
        a.should.have.property 'geographic', true
        a = plans.validate '+78124512345'
        a.should.have.property 'geographic', true
