<template>
  <div class="calculator">
    <div class="display">{{ state.current || '0'}}</div>
    <div class="btn" @click="clean">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="times">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot('.')">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
import { reactive } from 'vue'
export default {
    name: "Calculator",
    setup(){
      const state = reactive({
        current: '',
        previous: null,
        operatorCliked: false,
        op: null
      })
      function clean(){
        state.current = ''
      }
      function sign(){
        state.current = state.current.charAt(0) === '-'?state.current.slice(1):`-${state.current}`;
      }
      function percent(){
        state.current = `${parseFloat(state.current)/100}`
      }
      function append(number){
        if(state.operatorCliked === true){
          state.current = "";
          state.operatorCliked = false;
        }
        state.current = `${state.current}${number}`
      }
      function dot(){
        if(state.current.indexOf('.') !== -1){
          this.append('.')
        }
      }
      function setPrev(){
        state.previous = state.current
        state.operatorCliked = true
      }
      function operation(op,a,b){
        let result = 0
        switch(op){
          case '+':result = a+b;break;
          case '-':result = a-b;break;
          case '*':result = a*b;break;
          case '/':result = a/b;break;
            
        }
        return result
      }
      function  divide(){
        state.op = '/'
        setPrev()
        }
      function  times(){
        state.op = '*'
        setPrev()
      }
      function  minus(){
        state.op = '-'
        setPrev()
      }
      function  add(){
        state.op = '+'
          setPrev()
      }
      function equal(){
        state.current = operation(state.op,parseFloat(state.previous),parseFloat(state.current))
      }

      return{
        state,
        clean,
        sign,
        percent,
        append,
        add,
        times,
        minus,
        divide,
        equal,
        operation
      }
    }
   
}
</script>
