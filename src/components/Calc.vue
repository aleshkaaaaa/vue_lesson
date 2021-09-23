<template>
  <div class="calc">
    <div class="main">
      <input v-model.number ="op1" id="op1" type="number" v-focus />
      <input v-model.number ="op2" id="op2" type="number" v-focus />
      = {{ result }}
    </div>
    <div class="error">
      {{error}}
    </div>
    <div class="keyboard">
      <br>
      <button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('*')">*</button>
      <button @click="calculate('^')">^</button>
      <button @click="calculate('целочисленное деление')">целочисленное деление</button>
    </div>
    <div>
      <br>
      <input @click='toShow()' type="checkbox" id="checkbox" v-model="checked"> Отобразить экранную клавиатуру
    </div>
    <div class="inputKeyboard hidden-div">
      <div class="keybotdNumbers">
        <br>
        <button @click="typeLetter(0)">0</button>
        <button @click="typeLetter(1)">1</button>
        <button @click="typeLetter(2)">2</button>
        <button @click="typeLetter(3)">3</button>
        <button @click="typeLetter(4)">4</button>
        <button @click="typeLetter(5)">5</button>
        <button @click="typeLetter(6)">6</button>
        <button @click="typeLetter(7)">7</button>
        <button @click="typeLetter(8)">8</button>
        <button @click="typeLetter(9)">9</button>
        <button @click="deleteLastSym()">delete</button>
      </div>
      <div>
      <br>
        <input type="radio" id="one" value="Операнд 1" v-model="picked">Операнд 1
        <input type="radio" id="two" value="Операнд 2" v-model="picked">Операнд 2
        <br>
        <span>Выбрано: {{ picked }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  watch: {
    op1: function (val) {
      console.log('op1', val)
    },
    op2: function (val) {
      console.log('op2', val)
    },
    picked: function (val) {
      console.log('picked', val)
    }
  },
  updated () {
  },
  data () {
    return {
      op1: 0,
      op2: 0,
      error: '',
      result: 0,
      picked: 'Операнд 1',
      checked: false
    }
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    toShow () {
      if (this.checked === true) {
        document.querySelector('.inputKeyboard').classList.add('hidden-div')
      } else if (this.checked === false) {
        document.querySelector('.inputKeyboard').classList.remove('hidden-div')
      }
    },
    typeLetter (element) {
      if (this.picked === 'Операнд 1') {
        this.op1 += `${element}`
      } else if (this.picked === 'Операнд 2') {
        this.op2 += `${element}`
      }
    },
    deleteLastSym () {
      if (this.picked === 'Операнд 1') {
        this.op1 = this.op1.slice(0, -1)
      } else if (this.picked === 'Операнд 2') {
        this.op2 = this.op2.slice(0, -1)
      }
    },
    calculate (operation = '+') {
      switch (operation) {
        case '+':
          this.plus()
          break
        case '-':
          this.sub()
          break
        case '/':
          this.div()
          break
        case '*':
          this.multi()
          break
        case '^':
          this.degree()
          break
        case 'целочисленное деление':
          this.divToFull()
          break
      }
    },

    plus () {
      const { op1, op2 } = this
      this.result = op1 + op2
    },
    sub () {
      const { op1, op2 } = this
      this.result = op1 - op2
    },
    div () {
      const { op1, op2 } = this
      if (op2 === 0) {
        this.error = 'Делить на 0 нельзя!'
        return
      }
      this.result = op1 / op2
    },
    multi () {
      const { op1, op2 } = this
      this.result = op1 * op2
    },
    degree () {
      const { op1, op2 } = this
      this.result = Math.pow(op1, op2)
    },
    divToFull () {
      const { op1, op2 } = this
      this.result = Math.floor(op1 / op2)
    }
  }
}
</script>

<style scoped lang="scss">
  .hidden-div {
  display: none;
}
</style>
