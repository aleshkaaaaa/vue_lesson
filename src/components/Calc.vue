<template>
  <div class="calc">
    <div class="main">
      <input v-model.number ="op1" id="op1" type="number" />
      <input v-model.number ="op2" id="op2" type="number" />
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
      <input type="checkbox" id="checkbox" v-model="checked"> Отобразить экранную клавиатуру
    </div>
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
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      op1: 0,
      op2: 0,
      error: '',
      result: 0,
      picked: ''
    }
  },
  methods: {
    toShow () {
    },
    typeLetter (element) {
      if (document.getElementById('one').checked) {
        let text = document.getElementById('op1').value
        text += element
        document.getElementById('op1').value = text
      } else if (document.getElementById('two').checked) {
        let text = document.getElementById('op2').value
        text += element
        document.getElementById('op2').value = text
      }
    },
    deleteLastSym () {
      if (document.getElementById('one').checked) {
        let text = document.getElementById('op1').value
        text = text.slice(0, -1)
        document.getElementById('op1').value = text
      } else if (document.getElementById('two').checked) {
        let text = document.getElementById('op2').value
        text = text.slice(0, -1)
        document.getElementById('op2').value = text
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
