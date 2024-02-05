<script setup>
  import { ref } from 'vue';

const currentInput = ref('');
const operacao = ref('');
const resultado = ref('');

function adicionarNumero(numero) {
    if (operacao.value === '=') {
      currentInput.value = '';
      operacao.value = '';
    }
    currentInput.value += numero;
    atualizarDisplay();
  }

  function adicionarOperacao(op) {
    operacao.value = op;
    currentInput.value += op;
    atualizarDisplay();
  }

  function calcular() {
    if (currentInput.value !== '' && operacao.value !== '') {
      resultado.value = eval(currentInput.value);
      currentInput.value = resultado.value;
      operacao.value = '=';
      atualizarDisplay();
    }
  }

  function limpar() {
    currentInput.value = '';
    operacao.value = '';
    resultado.value = '';
    atualizarDisplay();
  }

  function atualizarDisplay() {
    resultado.value = operacao.value === '=' ? resultado.value : currentInput.value || '0';
  }

</script>

<template>
  <div id="app">
    <h1>Calculadora VueJS</h1>
    <div class="calculator">
      <div class="display">{{ resultado }}</div>
      <div class="buttons">
        <button @click="adicionarNumero(1)">1</button>
        <button @click="adicionarNumero(2)">2</button>
        <button @click="adicionarNumero(3)">3</button>
        <button @click="adicionarOperacao('+')">+</button>
        <button @click="adicionarNumero(4)">4</button>
        <button @click="adicionarNumero(5)">5</button>
        <button @click="adicionarNumero(6)">6</button>
        <button @click="adicionarOperacao('-')">-</button>
        <button @click="adicionarNumero(7)">7</button>
        <button @click="adicionarNumero(8)">8</button>
        <button @click="adicionarNumero(9)">9</button>
        <button @click="adicionarOperacao('*')">*</button>
        <button @click="adicionarNumero(0)">0</button>
        <button @click="limpar">C</button>
        <button @click="calcular">=</button>
        <button @click="adicionarOperacao('/')">/</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.calculator {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: 0 auto;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
}

.display {
  font-size: 24px;
  margin-bottom: 10px;
  padding: 5px;
  border: 1px solid #ccc;
  background-color: #fff;
  border-radius: 5px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 5px;
}

button {
  padding: 10px;
  font-size: 18px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #2980b9;
}
</style>
