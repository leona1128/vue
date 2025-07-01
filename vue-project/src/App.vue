<script setup>
import todoApp from './components/todoApp.vue'
import {ref} from 'vue';
const notes = ref([
  { id: 1, color: '#fff' },
])
</script>

<template>
  <main>
    <div id="notes">
      <todoApp
        v-for="note in notes"
        :key="note.id"
        :color="note.color"
      />
    </div>
  </main>
 

</template>
<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  background-color: #e1e1e1d6;
}

</style>
