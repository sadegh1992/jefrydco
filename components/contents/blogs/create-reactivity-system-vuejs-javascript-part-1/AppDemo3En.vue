<template>
  <app-demo :path="DEFAULT_PATH" :name="$options.name">
    <div class="demo-card demo-card-3">
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
        if (!window.state3) {
          // We put the code inside immediately invoked function expression to avoid polluting global variable
          // We also change the arrow function to anonymous function because the arrow function will serialized by Nuxt.
          window.state3 = (function () {
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
              const stateDisplay = document.querySelector('.demo-card-3 .state')
              stateDisplay.innerText = JSON.stringify(state, null, 2)

              const resultDisplay = document.querySelector(
                '.demo-card-3 .result'
              )
              resultDisplay.innerText = state.result.toString()
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
