<template>
  <div class="calculator">
    <div class="result" style="grid-area: result"></div>

    <!-- Operators -->
    <button style="grid-area: all-clean">AC</button>
    <button style="grid-area: pos-neg">+/-</button>
    <button style="grid-area: percent">%</button>
    <button style="grid-area: plus">+</button>
    <button style="grid-area: minus">-</button>
    <button style="grid-area: multiply">×</button>
    <button style="grid-area: divide">÷</button>
    <button style="grid-area: equal">=</button>

    <!-- digits -->
    <button style="grid-area: number-1">1</button>
    <button style="grid-area: number-2">2</button>
    <button style="grid-area: number-3">3</button>
    <button style="grid-area: number-4">4</button>
    <button style="grid-area: number-5">5</button>
    <button style="grid-area: number-6">6</button>
    <button style="grid-area: number-7">7</button>
    <button style="grid-area: number-8">8</button>
    <button style="grid-area: number-9">9</button>
    <button style="grid-area: number-0">0</button>

    <!-- decimal mark -->
    <button style="grid-area: dot-mark">.</button>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  $btn-width: 80px;
  $btn-height: 80px;

  .calculator {
    display: grid;
    grid-template-areas:
      "result result result result"
      "all-clean pos-neg percent divide"
      "number-7 number-8 number-9 multiply"
      "number-4 number-5 number-6 minus"
      "number-1 number-2 number-3 plus"
      "number-0 number-0 dot-mark equal";

    grid-template-columns: repeat(4, $btn-width);
    grid-template-rows: repeat(6, $btn-height);

    box-shadow: -8px -8px 16px -10px rgba(255, 255, 255, 1),
    8px 8px 16px -10px rgba(0, 0, 0, .15);
    padding: 24px;
    border-radius: 20px;

    button {
      display: inline-block;
      margin: 8px;
      padding: 0;
      border: 0;
      outline: none;
      border-radius: calc($btn-height / 4);
      font-family: "SF Pro Text", sans-serif;
      font-size: 24px;
      font-weight: normal;
      cursor: pointer;
      color: #999;

      background: linear-gradient(135deg, rgba(230, 230, 230, 1) 0%, rgba(246, 246, 246, 1) 100%);
      box-shadow: -4px -4px 10px -8px rgba(255, 255, 255, 1), 4px 4px 10px -8px rgba(0, 0, 0, .3);

      &:active {
        box-shadow: -4px -4px 10px -8px rgba(255, 255, 255, 1) inset, 4px 4px 10px -8px rgba(0, 0, 0, .3) inset;
      }
    }
  }

  .result {
    line-height: $btn-height;
    font-family: monospace;
    font-size: 48px;
    text-align: right;
    padding: 0 20px;
    color: #666;
  }
</style>
