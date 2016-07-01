    numbering_plans = require './plans'
    {numbering_plan_of,number_in,validate} = require './validate'

    @plans = numbering_plans
    @validate = (number) ->
      validate numbering_plans, number
    @numbering_plan_of = (number) ->
      numbering_plan_of numbering_plans, number
    @number_in = (number) ->
      number_in numbering_plans, number
