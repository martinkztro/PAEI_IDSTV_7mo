<script setup>
import { ref } from 'vue'

const count = ref(0)
let msg = ref("");
let num1 = ref(0);
let num2 = ref(0);
let resultado = ref(null);


function suma() {
  resultado.value = num1.value + num2.value;

  return resultado.value;
}
</script>
--------------------------
<template>

  <!-- CONTADOR -->
  <fieldset>
    <legend>CONTADOR</legend>
    <button type="button" v-on:click="count++">CLICK ME {{ count }}</button>
  </fieldset>

  <!-- MENSAJE DE SALUDO -->
  <h1>Hola {{ msg }}</h1>
  <fieldset>
    <legend>SALUDO</legend>
    <div>
      <input v-model="msg" />
    </div>
  </fieldset>

  <br>

  <!-- CALCULADOR DE SUMAS -->
  <fieldset>
    <legend>SUMADORA</legend>
    <div class="wrapper">
      <input v-model="num1" type="number" name="num1" id="num">
      <input v-model="num2" type="number" name="num2" id="">

      <button type="button" v-on:click="suma">RESULTADO</button>
    </div>

    <h2 v-if="resultado !== null">Resultado: {{ resultado }}</h2>
  </fieldset>

</template>