    chai = require 'chai'
    chai.should()
    describe 'To be done', ->
      {plans} = require '..'
      it 'should be listed with no plans', ->
        plans.should.have.property '8816'
        plans[8816].should.have.property 'name', 'Iridium'
        plans[8816].should.have.property 'plan'
        Object.getOwnPropertyNames(plans[8816].plan).should.have.length 0

        plans.should.have.property '998'
        plans[998].should.have.property 'name', 'Uzbekistan'
        plans[998].should.have.property 'plan'
        Object.getOwnPropertyNames(plans[998].plan).should.have.length 0
