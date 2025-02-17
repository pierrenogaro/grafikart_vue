<template>
<ul>
  <li>
    {{person.firstName}}
    {{person.lastName}}
    {{person.age}}
  </li>
</ul>
  <button @click.prevent="randomAge">changer age</button>
</template>

<script setup>
import {ref} from "vue";
const person = ref({
  firstName: "John",
  lastName: "Doe",
  age: 20,
})

const randomAge = () => {
  person.value = {
    ...person.value,
    age : Math.round(Math.random() * 100)
  }
}
</script>


<style>

</style>
