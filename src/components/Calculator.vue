<template>
  <div class="calculator">
      <div class="display border-top border-left border-right">{{ current }}</div>
      <div class="btn border-left border-top border-right" @click="clear()" >AC</div>
      <div class="btn border-top border-right" >+/-</div>
      <div class="btn border-top border-right" @click="percent">%</div>
      <div class="btn operator  " @click="divide">/</div>
      <div class="btn border-left border-top border-right" @click="append('7')" >7</div>
      <div class="btn border-top border-right" @click="append('8')" >8</div>
      <div class="btn border-top border-right" @click="append('9')" >9</div>
      <div class="btn operator border-top" @click="times" >x</div>
      <div class="btn border-left border-top border-right" @click="append('4')" >4</div>
      <div class="btn border-top border-right" @click="append('5')" >5</div>
      <div class="btn border-top border-right" @click="append('6')" >6</div>
      <div class="btn operator border-top" @click="minus" >-</div>
      <div class="btn border-left border-top border-right" @click="append('1')" >1</div>
      <div class="btn border-top border-right" @click="append('2')" >2</div>
      <div class="btn border-top border-right" @click="append('3')" >3</div>
      <div class="btn operator border-top" @click="add" >+</div>
      <div class="btn zero border-left border-top border-right border-bottom" @click="append('0')" >0</div>
      <div class="btn border-top border-right border-bottom" @click="dot">.</div>
      <div class="btn operator border-top border-bottom" @click="equal">=</div>
  </div>
</template>

<script>
  export default {
    name: 'Calculator',
    data() {
      return {
        beggin: true,
        previous: null,
        current:'0',
        operator: null,
        operatorClicked: false
      }
    },
    methods: {

      clear()
      {
        this.current = '0';
        this.beggin = true;
      },

      percent()
      {
        this.current = `${parseFloat(this.current)/ 100}`;
      },

      append(number)
      {
        if( this.operatorClicked || this.beggin ) 
        {
          this.current = '';
          this.operatorClicked = false;
          this.beggin = false; 
        }
        this.current = `${this.current}${number}`;
      },

      dot()
      {
        if(this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },

      setPrevious()
      {
        this.previous = this.current;
        this.operatorClicked = true;
      },

      divide()
      {
        this.operator = (a,b) => a / b;
        this.setPrevious();
      },

      times()
      {
        this.operator = (a,b) => a * b;
        this.setPrevious();
      },

      minus()
      {
        this.operator = (a,b) => a - b;
        this.setPrevious();
      },

      add()
      {
        this.operator = (a,b) => a + b;
        this.setPrevious();
      },

      equal()
      {
          this.current = `${ this.operator( parseFloat (this.previous), parseFloat(this.current))}`;
          this.previous = null;
      }

    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


  .operator
  {
    background: rgb(47, 47, 71);
    color: white;
    
  }

  .calculator
  {
    font-size: 24px;
    width: 400px;
    margin: 0 auto ;
    display: grid;
    grid-template-columns: repeat( 4, 1fr ) ;
    grid-auto-rows: minmax( 50px, auto );

  }

  .display
  {
    grid-column: 1 / 5;
    padding: 18px;
    background: rgba(221, 200, 200, 0.1);
  }

  .zero 
  {
    grid-column: 1 / 3
  }

    .border-left
  {
    border-left: solid 1px rgba(233, 233, 233, 0.8);
  }

    .border-right
  {
    border-right: solid 1px rgba(233, 233, 233, 0.8);
  }

    .border-top
  {
    border-top: solid 1px rgba(233, 233, 233, 0.8);
  }

    .border-bottom
  {
    border-bottom: solid 1px rgba(233, 233, 233, 0.8);
  }

  .btn
  {
    text-align: center;
    padding: 18px;
  }

  .btn:hover
  {
    background: rgb(221, 200, 200);
    cursor: pointer;
  }

</style>
