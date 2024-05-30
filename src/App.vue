<script setup>
import { reactive, computed } from 'vue';


const estado = reactive ({
  numero1: "",
  numero2: "",
  operacao: "soma"
})

const resultadoSoma = computed(() => {
  const num1 = parseFloat(estado.numero1) || 0;
  const num2 = parseFloat(estado.numero2) || 0;
  switch (estado.operacao) {
    case 'multi':
      return num1 * num2;
    case 'divi':
      return num2 !== 0 ? num1 / num2 : 'Erro: Divisão por zero';
    case 'soma':
    default:
      return num1 + num2;
  }
});

</script>

<template>
  <div class="painel">
    <select class="select" @change="e => estado.operacao = e.target.value">
      <option value="soma">Soma</option>
      <option value="multi">Multiplicação</option>
      <option value="divi">Divisão</option>
    </select>
    <div class="flex">
      <input @keyup="e => estado.numero1 = e.target.value" type="text" placeholder="Nº1">
      <span v-if="estado.operacao === 'soma'">+</span>
      <span v-if="estado.operacao === 'multi'">*</span>
      <span v-if="estado.operacao === 'divi'">/</span>
      <input @keyup="e => estado.numero2 = e.target.value" type="text" placeholder="Nº2">
    </div>
    <h1 class="resultado">Resultado: {{ resultadoSoma }}</h1>
  </div>
</template>

<style scoped>
  .painel {
    width: 100%;
    max-width: 300px;
    margin: auto;
    margin-top: 50px;
  }
  .select{
    width: 100%;
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }
  input {
    padding: 10px;
    width: 35%;
    border-radius: .3rem;
    border: 2px solid black;
    text-align: end;
    font-size: 1.5rem;
    font-weight: bold;
  }
  .flex{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
  }
  span{
    font-size: 2rem;
    font-weight: bold;
  }
  .resultado{
    text-align: center;
  }
</style>
