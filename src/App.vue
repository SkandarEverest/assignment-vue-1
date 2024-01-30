<script setup>
  import { ref } from 'vue';


const display = ref('');

function updateDisplay(value) {

  if (value === 'AC') {
    return display.value = '';
  }

  if (value === '=') {
    if (display.value === ''){
      return
    } 
    if (!['+', '-', '*', '/'].some(char => display.value.includes(char))){
      return
    } 
    if ( ['+', '-', '*', '/'].includes(display.value.slice(-1)) ){
      return
    }
    return display.value = String(eval(display.value));

  }
    
  if ( ['+', '*', '/'].includes(value) && display.value === '' ){
    return
  }
  
  if ( ['+', '-', '*', '/'].includes(value) && ['+', '-', '*', '/'].includes(display.value.slice(-1)) ){
    return
  }
    
  display.value += value;
  }
  
</script>

<template>
  <div class="d-flex flex-column min-vh-100 justify-content-center align-items-center">

    <div class="calculator card" style="background-color: darkgray;border-radius: 10px">
      
      <input type="text" class="calculator-screen z-depth-1" style="border-radius: 10px 10px 0px 0px; " value="" v-model="display" disabled />
      
      <div class="calculator-keys">
        
        <button type="button" class="operator btn btn-info" @click="updateDisplay('+')">+</button>
        <button type="button" class="operator btn btn-info" @click="updateDisplay('-')">-</button>
        <button type="button" class="operator btn btn-info" @click="updateDisplay('*')">&times;</button>
        <button type="button" class="operator btn btn-info" @click="updateDisplay('/')">&divide;</button>
        
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('7')">7</button>
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('8')">8</button>
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('9')">9</button>
        
        
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('4')">4</button>
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('5')">5</button>
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('6')">6</button>
        
        
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('1')">1</button>
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('2')">2</button>
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('3')">3</button>
        
        
        <button type="button" class="btn btn-light waves-effect" @click="updateDisplay('0')">0</button>
        <button type="button" class="decimal function btn btn-secondary" @click="updateDisplay('.')">.</button>
        <button type="button" class="all-clear function btn btn-danger btn-sm" @click="updateDisplay('AC')">AC</button>
        
        <button type="button" class="equal-sign operator btn btn-warning opacity-75" @click="updateDisplay('=')">=</button>
        
      </div>
    </div>
  </div>
    
</template>

<style scoped>

.calculator {
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 400px;
}

.calculator-screen {
  width: 100%;
  height: 80px;
  border: none;
  background-color: #252525;
  color: #fff;
  text-align: right;
  padding-right: 20px;
  padding-left: 10px;
  font-size: 4rem;
}

button {
  height: 60px;
  font-size: 2rem!important;
}

.equal-sign {
  height: 100%;
  grid-area: 2 / 4 / 6 / 5;
}

.calculator-keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
  padding: 20px;
}

</style>
