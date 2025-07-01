<script setup>
import todoApp from './components/todoApp.vue';
import addList from './components/addList.vue';
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
  <addList/>
  
 

</template>
<style scoped>
template {

  height: 100vh;
  width: 100vw;
  background-color: #e1e1e1d6;
}
main{
  width:100%;
  height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
