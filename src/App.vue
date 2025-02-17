<template>
  <h1>Bonjour {{firstName.toUpperCase()}}</h1>
  <p>Comment allez vous ?</p>
  <p :class="{active : true}">Compteur : {{count}} <div v-html="lastName"></div></p>
  <div v-if="count >= 5">
    <h1>Bravo, 10 CLICKS !!!</h1>
  </div>
  <div v-else>
    <h1>Vous avez cliqué moins de 5 fois</h1>
  </div>
  <button @click="increment">+</button>
  <button @click="decrement">-</button>
  <ul>
    <li
        v-for="movie in movies" :key="movie">
      {{movie}}<button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>

  <button @click="sortMovies">Réorganiser</button>

  <form action="" @submit.prevent="addMovie">
    <input type="text" placeholder="nouveau film" v-model="movieName">
    {{movieName}}
    <button>Ajouter</button>
  </form>
</template>

<script setup>
  import {ref} from "vue";

  const firstName = "John"
  const lastName = '<span>demo</span>'
  const count = ref(0)
  const movieName = ref('')
  const movies = ref([
      'Matrix',
      'Lilo & Stitch',
      'Harry Potter'
  ])
  console.log(count, count.value)
  const increment = () => {
    count.value++
  }

  const decrement = () => {
    count.value--
  }

  const deleteMovie = (movie) => {
    movies.value = movies.value.filter(m => m !== movie)
  }

  const sortMovies = () => {
    movies.value.sort((a, b) => a > b ? 1 : -1)
  }

  const addMovie = (event) => {
    event.preventDefault()
    movies.value.push(movieName.value)
    movieName.value = ""
  }
</script>

<style>
h1 {
  color: blue;
}

.active{
  color: red;
}
</style>
