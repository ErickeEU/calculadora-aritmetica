<script setup>
import { reactive } from 'vue';

  
  const state = reactive({
    operation: 'Adição',
    tag: '',
    values: {
      value1: 0,
      value2: 0
    },
    result: null

  })
  
  function getTag() {
    let { operation } = state
    switch (operation) {
      case 'Adição' :
        return '+'
      case 'Subtração':
        return '-'
      case 'Multiplicação':
        return 'x'
      case 'Divisão':
        return '/'
    }
  }

  function calc() {
    let { operation } = state
    switch (operation) {
      case 'Adição':
        return Number(state.values.value1) + Number(state.values.value2)
      case 'Subtração':
        return state.values.value1 - state.values.value2
      case 'Multiplicação':
        return state.values.value1 * state.values.value2
      case 'Divisão':
        return state.values.value1 / state.values.value2
    }
  }

  function getResult() {
    state.result = calc()
  }

</script>

<template>
<header>
    <h1 class="text-center">Calculadora Aritmética</h1>
</header>
<div class="container">
<form class="p-3 text-center" action="">
  <label class="me-2" for="input">Selecione a operação:</label>
  <select @change="event => state.operation = event.target.value" name="" id="input">
    <option value="Adição">Adição</option>
    <option value="Subtração">Subtração</option>
    <option value="Divisão">Divisão</option>
    <option value="Multiplicação">Multiplicação</option>
  </select>
</form>
<form @submit.prevent="getResult()" class="text-center">
  <div class="row justify-content-center align-items-center">
    <div class="col-1">
      <input @keyup="event => state.values.value1 = event.target.value" type="number" class="form-control form-control-sm input">
    </div>
    <div class="col-auto"><span class="p-2 fw-bold">{{ getTag() }}</span></div>
    <div class="col-1">
      <input @keyup="event => state.values.value2 = event.target.value" type="number" class="form-control form-control-sm input">
    </div>
    <div class="col-auto">
      <span class="fw-bold">=</span>
    </div>
    <div class="text-center col-auto">
      <span class="fw-bold fs-3">{{ calc() }}</span>
    </div>
  </div>
</form>
</div>
</template>

<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type=number] {
  -moz-appearance: textfield;
}
</style>
