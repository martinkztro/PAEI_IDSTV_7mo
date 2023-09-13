<script setup>
import { ref } from 'vue'

let name = ref("");
let lastname = ref("");
let persons = ref([]);

function savePerson() {
  console.log("hola");

  let person = {
    firstName: name.value,
    lastName:  lastname.value
  }

  console.log(person);

  persons.value.push(person);
}



</script>
--------------------------
<template>

  <form action="">

    <fieldset>
      <legend>Nombre</legend>
      <input placeholder="Write here..." v-model="name" type="text" name="" id="">
    </fieldset>

    <fieldset>
      <legend>Lastname</legend>
      <input placeholder="Write here..." v-model="lastname" type="text" name="" id="">
    </fieldset>

    <button v-on:click="savePerson" type="button">Save Data</button>
  </form>

  <ol>
    <li v-for="p in persons">
      {{p.value}} {{p.lastName}}
    </li>
  </ol>


</template>