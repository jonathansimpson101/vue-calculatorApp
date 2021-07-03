<template>
<body>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div class="button" v-on:click="clear">AC</div>
    <div class="button" v-on:click="sign">+/-</div>
    <div class="button" v-on:click="percent">%</div>
    <div class="button operator" v-on:click="divide">/</div>
    <div class="button" v-on:click="append(7)">7</div>
    <div class="button" v-on:click="append(8)">8</div>
    <div class="button" v-on:click="append(9)">9</div>
    <div class="button operator" v-on:click="times">x</div>
    <div class="button" v-on:click="append(4)">4</div>
    <div class="button" v-on:click="append(5)">5</div>
    <div class="button" v-on:click="append(6)">6</div>
    <div class="button operator" v-on:click="minus">-</div>
    <div class="button" v-on:click="append(1)">1</div>
    <div class="button" v-on:click="append(2)">2</div>
    <div class="button" v-on:click="append(3)">3</div>
    <div class="button operator" v-on:click="add">+</div>
    <div class="button zero" v-on:click="append(0)">0</div>
    <div class="button" v-on:click="dot">.</div>
    <div class="button operator" v-on:click="equal">=</div>
  </div>
</body>
</template>

<style>
  body{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width:  100vw;
    font-family: Helvetica;
  }

  .calculator{
    width:  200px;
    height:  300px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    border: 1px solid black;
  }

  .display{
    grid-column:  1 / span 4;
    padding-right:  10px;
    border:  1px solid black;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    background-color:  lightgrey;
    text-align: right;
  }

  .button{
    border:  1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .zero{
    grid-column:  1 / span 2;
  }

  .operator{
    background-color: orange;
    color:  #fff;
  }
</style>

<script>
  export default {

    name: 'calculator',

    data () {
      return {
        current: '',
        previous: null,
        operator: null,
        operatorClicked: false
      }
    },
    methods: {
      append (value) {
        if(this.operatorClicked){
          this.current = '';
          this.operatorClicked = false;
        }
        return this.current += value;
      },
      clear(){
        return this.current = ''
      },
      sign(){
        if(this.current !== '0'){
        return this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
        }
      },
      percent(){
        this.current = `${parseFloat(this.current) / 100}`
      },
      dot(){
        if(this.current.indexOf('.') === -1){
          this.append('.');
        }
      },
      setPrevious(){
        this.operatorClicked = true;
        this.previous = this.current;
      },
      divide(){
        this.operator = (a, b) => a / b;
        this.setPrevious();
      },
      times(){
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },
      add(){
        this.operator = (a, b) => a + b;
        this.setPrevious();
      },
      minus(){
        this.operator = (a, b) => a - b;
        this.setPrevious();
      },
      equal(){
        this.current = `${this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
          )}`;
      }
    }
  }
</script>
