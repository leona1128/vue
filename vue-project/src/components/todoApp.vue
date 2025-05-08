<script setup>
import { ref, computed } from 'vue'


const todos= ref([]);
const date = ref('2025.04.22');
const showInput = ref(false);
let add = ref('');
const newTodo = ref('');
const toggleInput = () => {
  showInput.value = !showInput.value;

  // 切換顯示狀態，原本是false，點擊後變成true
}
const addSymbol = computed(() => (showInput.value ? '🫵🏻' : '➕'))
function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value = newTodo.value.trim()

    newTodo.value = '';
    showInput.value = false;
  }
}


</script>

<template>
  <div class="container">
  <div class="title">
    <h1>我的便利貼</h1>
    <h2>日期：{{date}}</h2>
  </div>
   

    <!-- 代辦事項 -->
     <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" :id="'todo-' + index" v-model="todo.completed"  />
        <label :for="'todo-' + index">{{ todo }}</label>
      </li>
     </ul>
    <!-- 新增事項 -->
     <div class="newListIcon">
      <div class="add" @click="toggleInput">{{ addSymbol }}</div>
      <template v-if="showInput">

      <input type="text" v-model="newTodo" placeholder="請輸入代辦事項"@keyup.enter="addTodo"  />
      <button @click="addTodo">新增</button>
      </template>
      <div class="delete">🗑️</div>
     </div>
   
  </div>
</template>

<style scoped>
.container{
  max-width: 600px;
    max-height: 600px;
    width: 300px;
    height: 300px;
    background-color: #fff;
    border-radius: 0  0 10px 10px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    position: relative;
}
.title{
  display: flex;
  align-items: flex-end;
  margin-bottom: 20px;
}
h1{
  font-size: 24px;
  padding-right: 10px;
}
h2{
  font-size: 12px;

}
ul{
  padding: 5px;
  list-style: none;
}
label{
  padding-right: 10px;
}
.newListIcon{
  display: flex;
  align-items: center;
  position: absolute;
  bottom: 3px;
  right: 8px;
  font-size: 24px;
  cursor: pointer;
}
.add{
  padding:0 5px;

}

</style>
