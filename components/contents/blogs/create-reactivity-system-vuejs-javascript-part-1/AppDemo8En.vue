<template>
  <app-demo :path="DEFAULT_PATH" :name="$options.name">
    <div class="demo-card demo-card-8">
      <pre class="state"></pre>

      <input type="number" class="input1" min="0" />
      <select class="operator">
        <option value="+">&plus;</option>
        <option value="-">&minus;</option>
        <option value="*">&times;</option>
        <option value="/">&divide;</option>
      </select>
      <input type="number" class="input2" min="0" />

      <div class="result"></div>

      <script>
        if (!window.state8) {
          // We put the code inside immediately invoked function expression to avoid polluting global variable
          // We also change the arrow function to anonymous function because the arrow function will serialized by Nuxt.
          window.state8 = (function () {
            const OPERATOR = {
              PLUS: '+',
              SUBSTRACT: '-',
              MULTIPLY: '*',
              DIVIDE: '/'
            }

            const state = {
              result: 0,
              operator: OPERATOR.PLUS,
              input1: 0,
              input2: 0
            }

            function main() {
              // We have to prefixed the selector in accordance with the root component class
              // It avoids the script to be applied to all demo
              const tampilanKeadaan = document.querySelector(
                '.demo-card-8 .state'
              )

              const tampilanHasil = document.querySelector(
                '.demo-card-8 .result'
              )

              const tampilanInput1 = document.querySelector(
                '.demo-card-8 .input1'
              )
              const tampilanInput2 = document.querySelector(
                '.demo-card-8 .input2'
              )

              const tampilanOperator = document.querySelector(
                '.demo-card-8 .operator'
              )

              function updateDisplay() {
                tampilanKeadaan.innerText = JSON.stringify(state, null, 2)
                tampilanHasil.innerText = state.result.toString()

                tampilanInput1.value = state.input1.toString()
                tampilanInput2.value = state.input2.toString()

                tampilanOperator.value = state.operator
              }

              function calculateResult() {
                switch (state.operator) {
                  case OPERATOR.PLUS:
                    state.result = state.input1 + state.input2
                    break
                  case OPERATOR.SUBSTRACT:
                    state.result = state.input1 - state.input2
                    break
                  case OPERATOR.MULTIPLY:
                    state.result = state.input1 * state.input2
                    break
                  case OPERATOR.DIVIDE:
                    state.result = state.input1 / state.input2
                    break
                  default:
                    break
                }
              }

              updateDisplay()

              tampilanInput1.addEventListener('input', function (event) {
                const targetInput1 = event.target
                state.input1 = parseInt(targetInput1.value)
                calculateResult()
                updateDisplay()
              })
              tampilanInput2.addEventListener('input', function (event) {
                const targetInput2 = event.target
                state.input2 = parseInt(targetInput2.value)
                calculateResult()
                updateDisplay()
              })

              tampilanOperator.addEventListener('change', function (event) {
                const targetOperator = event.target
                const selectedOperator = targetOperator.selectedOptions[0].value
                state.operator = selectedOperator
                calculateResult()
                updateDisplay()
              })
            }

            // We have to run the method because this script is executed inside vue component
            // document.addEventListener('DOMContentLoaded', main)
            main()

            return state
          })()
        }
      </script>
    </div>
  </app-demo>
</template>

<script>
import AppDemoBase from './AppDemoBase'

export default {
  extends: AppDemoBase
}
</script>
