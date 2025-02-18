<template>
  <div ref="div">
    Temps : {{time}}
    Largeur : {{size.width}}, Haureur : {{size.height}}
  </div>

</template>

<script setup>
import {onMounted, onUnmounted, ref} from "vue";
import timer from "@/Timer.vue";

const time = ref(0)
const size = ref({width: 0, height: 0})
const div = ref(null)

onMounted(() => {
  const rect = div.value.getBoundingClientRect()
  size.value = {width : rect.width, height : rect.height}
  setInterval(() => {
    time.value++
  }, 1000)
})

onUnmounted(()=> {
  clearInterval(timer)
})
</script>