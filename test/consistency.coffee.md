    chai = require 'chai'
    chai.should()

    numbering_plans = require '..'

    for own cc, data of numbering_plans.plans
      do (cc,data) ->
        describe "#{cc}", ->
          it 'should have a name', ->
            data.should.have.property 'name'
          it 'should have a plan', ->
            data.should.have.property 'plan'

        for own prefix, plan of data.plan
          do (prefix,plan) ->

            describe "CC #{cc} NSN prefix #{prefix}", ->

              count = (args...) ->
                members = 0
                for type in args
                  do (type) ->
                    if plan[type]
                      members += 1
                      plan.should.have.property type, true
                members

              it 'should have min, unless it is blocked', ->
                unless plan.block
                  plan.should.have.property 'min'
                  plan.min.should.be.at.least 1
                  plan.min.should.be.at.most 16
              it 'should have max, unless it is blocked', ->
                unless plan.block
                  plan.should.have.property 'max'
                  plan.max.should.be.at.least 1
                  plan.max.should.be.at.most 16
              it 'min should be at most max, unless it is blocked', ->
                unless plan.block
                  plan.should.have.property 'min'
                  plan.should.have.property 'max'
                  plan.min.should.be.at.most plan.max

              it 'should have a single type, unless it is blocked', ->
                if plan.block
                  plan.should.have.property 'block', true
                  # plan.should.not.contain.any.keys 'fixed', 'mobile', 'mixed', 'special', 'value_added'
                else
                  plan.should.contain.any.keys 'fixed', 'mobile', 'mixed', 'special', 'value_added'
                  count('fixed','mobile','mixed','special','value_added').should.equal 1

              it 'should only have geographic if it is fixed or mixed', ->
                if plan.geographic
                  count('fixed','mixed').should.equal 1
              it 'should only have corporate if it is fixed or mixed', ->
                if plan.corporate
                  count('fixed','mixed').should.equal 1

              it 'should only have freephone it if is value_added', ->
                if plan.freephone
                  plan.should.have.property 'value_added', true
              it 'should only have shared_cost it if is value_added', ->
                if plan.shared_cost
                  plan.should.have.property 'value_added', true
              it 'should only have personal it if is value_added', ->
                if plan.personal
                  plan.should.have.property 'value_added', true
              it 'should only have premium it if is value_added', ->
                if plan.premium
                  plan.should.have.property 'value_added', true
              it 'should only have adult it if is value_added', ->
                if plan.adult
                  plan.should.have.property 'value_added', true

              it 'should not be both freephone, shared_cost, or premium', ->
                count('freephone','shared_cost','premium').should.be.at.most 1

              it 'should not be both personal and adult', ->
                count('personal','adult').should.be.at.most 1

              it 'should only have voicemail it if is special', ->
                if plan.voicemail
                  plan.should.have.property 'special', true
              it 'should only have test it if is special', ->
                if plan.test
                  plan.should.have.property 'special', true
              it 'should only have vpn it if is special', ->
                if plan.vpn
                  plan.should.have.property 'special', true
              it 'should only have emergency it if is special', ->
                if plan.emergency
                  plan.should.have.property 'special', true

              it 'should only be one of voicemail, test, vpn, or emergency', ->
                count('voicemail','test','vpn','emergency').should.be.at.most 1
