<template>
  <div class="calculator">
    <div class="result" style="grid-area: result">
      {{ result }}
    </div>

    <!-- Operators -->
    <button style="grid-area: all-clean"
            @click="clear">AC</button>
    <button style="grid-area: pos-neg"
            @click="calculateToggle">+/-</button>
    <button style="grid-area: percent"
            @click="calculatePercentage">%</button>
    <button style="grid-area: plus"
            @click="append('+')">+</button>
    <button style="grid-area: minus"
            @click="append('-')">-</button>
    <button style="grid-area: multiply"
            @click="append('*')">×</button>
    <button style="grid-area: divide"
            @click="append('/')">÷</button>
    <button style="grid-area: equal"
            @click="calculate">=</button>

    <!-- digits -->
    <button style="grid-area: number-1"
            @click="append('1')">1</button>
    <button style="grid-area: number-2"
            @click="append('2')">2</button>
    <button style="grid-area: number-3"
            @click="append('3')">3</button>
    <button style="grid-area: number-4"
            @click="append('4')">4</button>
    <button style="grid-area: number-5"
            @click="append('5')">5</button>
    <button style="grid-area: number-6"
            @click="append('6')">6</button>
    <button style="grid-area: number-7"
            @click="append('7')">7</button>
    <button style="grid-area: number-8"
            @click="append('8')">8</button>
    <button style="grid-area: number-9"
            @click="append('9')">9</button>
    <button style="grid-area: number-0"
            @click="append('0')">0</button>

    <!-- decimal mark -->
    <button style="grid-area: dot-mark"
            @click="append('.')">.</button>
  </div>
</template>

<script>
export default {
  name: 'Calculator',

  data: function() {
    return {
      result: '0',
      isDecimalAdded: false,
      isOperatorAdded: false,
      isStarted: false,
    }
  },

  methods: {
    // When pressing "AC"
    clear() {
      this.result = '0';
      this.isDecimalAdded = false;
      this.isOperatorAdded = false;
      this.isStarted = false;
    },

    // Check if the character is + | - | * | /
    isOperator(char) {
      return ['+', '-', '*', '/'].indexOf(char) > -1;
    },

    // When pressing operator or button with digit
    append(char) {
      if (this.result === '0' && !this.isOperator(char)) {
        if (char === '.') {
          this.result += '' + char;
          this.isDecimalAdded = true;
        } else {
          this.result = '' + char;
        }
        this.isStarted = true;
        return;
      }

      // If digit
      if (!this.isOperator(char)) {
        if (char === '.' && this.isDecimalAdded) return;

        if (char === '.') {
          this.isDecimalAdded = true;
          this.isOperatorAdded = true;
        } else {
          this.isOperatorAdded = false;
        }

        this.result += '' + char;
      }

      // Add Operator
      if (this.isOperator(char) && !this.isOperatorAdded) {
        this.result += '' + char;
        this.isDecimalAdded = false;
        this.isOperatorAdded = true;
      }
    },

    // When pressing "="
    calculate() {
      let result = this.result;
      this.result = parseFloat(eval(result).toFixed(9)).toString();
      this.isDecimalAdded = false;
      this.isOperatorAdded = false;
    },

    // When pressing "+/-"
    calculateToggle() {
      if (this.isOperatorAdded || !this.isStarted || this.result === '0') return;

      this.result += '* - 1';
      this.calculate();
    },

    // When pressing "%"
    calculatePercentage() {
      if (this.isOperatorAdded || !this.isStarted || this.result === '0') return;

      this.result += '* 0.01';
      this.calculate();
    },
  }
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
