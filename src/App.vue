<template>
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
      <li v-for="todo in todos"
      :key="todo.date"
      :class="{completed : todo.completed }"
      >
        <label>
          <input type="checkbox" v-model="todo.completed">
          {{todo.title}}
        </label>
      </li>
    </ul>
    <div>
      <label for="">
        <input type="checkbox" v-model="hideCompleted">
        Masquer les tâches complétées
      </label>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
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

const sortedTodos = () => {
  return todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
}

</script>


<style>
.completed {
  opacity: .5;
  text-decoration: line-through;
}

</style>
