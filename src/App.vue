<template>
  <layout>
    <template v-slot:header>
      en tete

    </template>

    <template v-slot:aside>
     sidebar

    </template>

    <template v-slot:main>
     main

    </template>

    <template v-slot:footer>
     footer

    </template>
  </layout>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input type="text"
      v-model="newTodo"
      placeholder="Tâche à effectuer">
      <button :disabled="newTodo.length === 0">Ajouter la tache</button>
    </fieldset>
  </form>

  <div v-if="todos.length === 0"> Vous n'avez pas de tache à faire</div>
  <div v-else>
    <ul>
      <li v-for="todo in sortedTodos"
      :key="todo.date"
      :class="{completed : todo.completed }"
      >
        <label>
          <Checkbox :label="todo.title"
            v-model="todo.completed"
          />
        </label>
      </li>
    </ul>
    <div>
      <label for="">
        <input type="checkbox" v-model="hideCompleted">
        Masquer les tâches complétées
      </label>
      <p v-if="remainingTodos > 0">
        {{remainingTodos}} tâche{{remainingTodos > 1 ? 's' :''}} à faire
      </p>
    </div>
    <Checkbox :label="'Bonjour'"/>
  </div>
</template>

<script setup>
import {computed, ref} from "vue";
import Checkbox from "@/Checkbox.vue";
import Button from "@/Button.vue"
import Layout from "@/Layout.vue";

const newTodo = ref([])
const hideCompleted = ref(false);
const todos = ref([{
  title : 'Tache de test',
  completed: true,
  date: 1,
}, {
    title : 'Tache à faire',
    completed: false,
    date: 2,
  }])
const addTodo = () => {
  todos.value.push({
    title : newTodo.value,
    completed: true,
    date : Date.now()
  })
  newTodo.value = ''
}

const sortedTodos =  computed(() => {
  const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1);

  if (hideCompleted.value === true) {
    return sortedTodos.filter(t => t.completed === false);
  }

  return sortedTodos;
})

const remainingTodos = computed(() => {
  return todos.value.filter ( t => t.completed === false).length
})


</script>


<style>
.completed {
  opacity: .5;
  text-decoration: line-through;
}

</style>
