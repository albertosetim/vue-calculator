<template>
  <div class="calculator">
      <div class="display border-top border-left border-right">
        <p v-if="history.length == 0" >History clear</p>
        <ul class="history-list">
          <li v-for=" ( item, index ) in history" :key="index" class="history-list-item">
            <div class="history-item-container">
              <div class="item-opeartion">
                {{ item.operation }}
              </div>
              <div class="item-result">
                {{ item.result }}
              </div>
            </div>
          </li>
        </ul>
        {{ current_operation }} {{current_result}}
      </div>
      <div class="btn border-left border-top border-right" @click="clear()">C</div>
      <div class="btn border-top border-right" >+/-</div>
      <div class="btn border-top border-right" @click="operator('%')" >%</div>
      <div class="btn operator " @click="operator('/')" >/</div>
      <div class="btn border-left border-top border-right" @click="number('7')">7</div>
      <div class="btn border-top border-right" @click="number('8')">8</div>
      <div class="btn border-top border-right" @click="number('9')">9</div>
      <div class="btn operator border-top" @click="operator('*')">x</div>
      <div class="btn border-left border-top border-right" @click="number('4')">4</div>
      <div class="btn border-top border-right"  @click="number('5')">5</div>
      <div class="btn border-top border-right"  @click="number('6')">6</div>
      <div class="btn operator border-top"  @click="operator('-')" >-</div>
      <div class="btn border-left border-top border-right"  @click="number('1')">1</div>
      <div class="btn border-top border-right"  @click="number('2')">2</div>
      <div class="btn border-top border-right"  @click="number('3')">3</div>
      <div class="btn operator border-top" @click="operator('+')" >+</div>
      <div class="btn zero border-left border-top border-right border-bottom" @click="number('0')">0</div>
      <div class="btn border-top border-right border-bottom" @click="dot()">.</div>
      <div class="btn operator border-top border-bottom" @click="resolve()">=</div>
  </div>
</template>

<script>
  export default {
    name: 'Calculator',
    data() {
      return {
        current_operation : '',
        current_result : '0',
        current_operator : '',
        history : [],
        result  : '',
        preview : '' 
      }
    },
    methods: {

      

      /* Operator pressed */

      operator(op)
      {

        this.current_result = '';
        
        if(this.current_operation)
        {
          this.current_operation = this.current_operation + ' ' + op + ' ';
          this.current_operator = op;
        }
      },
  
      /* Number pressed */

      number( number )
      {
        this.current_result = '';

        if(this.current_operation && this.current_operation != "0")
        {
          this.current_operation = this.current_operation + number;
        }
        else
        {
          this.current_operation = number;
        }

        
      },

      dot()
      {
        if(this.current.indexOf('.') === -1) {
          this.current_operation = this.current_operation + '.';
        }
      },

      /* Add to history */

      add_history () 
      {
        this.history.push({ operation: this.current_operation, result: this.current_result });
      },

      /* clear from history */

      clear_history () 
      {
        this.history = [];
      },

      /* Print the screen preview */

      print_preview () 
      {

      },


      /* Clear screen and reset to zero ( "0" ) */

      clear()
      {
        this.current_operation = '';
        this.current_result = '0';

        this.clear_history();
      },


      /* resolve the string */
      resolve()
      {
          this.current_result = '= ' + eval(this.current_operation);
          this.add_history();
          
      }



/*  
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
 */
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

  ul{
    list-style: none;
    width: 100%;
    box-sizing: border-box;
    font-size: 12px;
    color: rgb(112, 111, 111);  
    padding: 0px;
    margin: 0px;  
    border-bottom: solid 1px rgba(221, 200, 200, 0.4);
    padding-bottom: 12px;
    margin-bottom: 12px;
  }

  li
  {
    width: 100%;
    box-sizing: border-box;

  }

  .history-item-container
  {
    display: flex;
    align-content: center;
    justify-items: center;
    padding: 3px;
  }

  .item-opeartion
  {
      text-align: left;
      min-width: 70%;
  }

    .item-result
  {
      text-align: right;
      min-width: 30%;
  }




</style>
