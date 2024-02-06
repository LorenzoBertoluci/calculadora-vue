<script setup>
  import { ref } from 'vue';

const valorAtual = ref('');
const operacao = ref('');
const resultado = ref(0);



const numero1 = ref(0);
const numero2 = ref(0);
const operacao1 = ref('+');
const results = ref(0);

function calcular1() {
    switch (operacao1.value) {
        case '+':
            results.value = numero1.value + numero2.value;
            break;
        case '-':
            results.value = numero1.value - numero2.value;
            break;
        case '*':
            results.value = numero1.value * numero2.value;
            break;
        case '/':
            results.value = numero1.value / numero2.value;
            break;
        default:
            results.value = 0;
    }
}



function adicionarNumero(numero) {
    if (operacao.value === '=') {
      valorAtual.value = '';
      operacao.value = '';
    }
    valorAtual.value += numero;
    atualizarDisplay();
  }

  function adicionarOperacao(op) {
    operacao.value = op;
    valorAtual.value += op;
    atualizarDisplay();
  }

  function calcular() {
    if (valorAtual.value !== '' && operacao.value !== '') {
      resultado.value = eval(valorAtual.value);
      valorAtual.value = resultado.value;
      operacao.value = '=';
      atualizarDisplay();
    }
  }

  function limpar() {
    valorAtual.value = '';
    operacao.value = '';
    resultado.value = '';
    atualizarDisplay();
  }

  function atualizarDisplay() {
    resultado.value = operacao.value === '=' ? resultado.value : valorAtual.value || '0';
  }

</script>

<template>

<div id="app1">
    <h1>Calculadora VueJS simples</h1>
    <div class="calculator">
      <input v-model="numero1" type="number" @click="calcular1" />
      <select v-model="operacao1" @change="calcular1">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">x</option>
        <option value="/">/</option>
      </select>
      <input v-model="numero2" type="number"  @click="calcular1"/>
      <div class="results">Resultado: {{ results }}</div>
    </div>
  </div>

  <div id="app">
    <h1>Calculadora VueJS completa</h1>
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

#app1 {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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

input,
select {
  margin: 10px 0;
  padding: 8px;
  font-size: 16px;
}

.results {
  margin-top: 20px;
  font-size: 18px;
}
</style>
