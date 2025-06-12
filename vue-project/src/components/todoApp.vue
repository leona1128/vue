<script setup>
import { ref, computed,onMounted } from 'vue'
const editingIndex = ref(null); // 正在編輯哪一筆
const editingText = ref('');    // 編輯中的文字內容

const isEditingDate = ref(false);
const editingDateText = ref('');
const todos= ref([]);
const date = ref('2025.04.22');
const showInput = ref(false);
const undone = computed(() => {
  return todos.value.filter(todo => !todo.completed).length;
  // filter()方法創建一個新數組，包含所有不符合條件的元素
});

const newTodo = ref('');
onMounted(() => {
  const storedTodos = localStorage.getItem('todos');
  if (storedTodos) {
    todos.value = JSON.parse(storedTodos);
    }
  const locaDate = localStorage.getItem('date');
  if (locaDate) {
    date.value = JSON.parse(locaDate);
  }
    });
const toggleInput = () => {
  showInput.value = !showInput.value;

  // 切換顯示狀態，原本是false，點擊後變成true
}
const addList = computed(() => (showInput.value ? '🫵🏻' : '➕'))
function addTodo() {
  if (newTodo.value.trim() !== '') {
    //trim()移除字符串兩端（開頭和結尾）的空白字符
    todos.value.push({
      text: newTodo.value.trim(),
      completed: false
    });
    newTodo.value = '';
    showInput.value = false;
    storedTodos();
  }
}
function storedTodos() {
  localStorage.setItem('todos', JSON.stringify(todos.value));
  // 將當前的todos數組存儲到localStorage中
}

function deleteTodo(index) {
  todos.value.splice(index, 1);
  // splice()方法從數組中添加或刪除元素
  storedTodos();
}
function editTodo(index) {
  editingIndex.value = index;
  editingText.value = todos.value[index].text;
  // 將正在編輯的索引和文本設置為當前待辦事項
}
function saveEdit(index) {
  if (editingText.value.trim() !== '') {// 確保編輯的文本不為空
    todos.value[index].text = editingText.value.trim();// 更新待辦事項的文本
    editingIndex.value = null;    // 清除正在編輯的索引
    editingText.value = '';   // 清除編輯中的文本
    storedTodos();
  }
}
function editdate() {
  isEditingDate.value = true;
  editingDateText.value = date.value;
  // 將日期設置為正在編輯的文本
}
function saveDate() {
  if (editingDateText.value.trim() !== '') {// 確保編輯的文本不為空
    date.value = editingDateText.value.trim(); // 更新待辦事項的文本
    isEditingDate.value = false;    // 清除正在編輯的索引
    editingDateText.value = '';   // 清除編輯中的文本
    locaDate()
  }

}

function locaDate(){
  localStorage.setItem('date', JSON.stringify(date.value));
}


</script>

<template>
  <div class="container">
  <div class="title">
    <h1>我的便利貼</h1>
    <h2>
  <template v-if="isEditingDate">
    <input 
      v-model="editingDateText" 
      @keyup.enter="saveDate"
      @blur="saveDate"
      type="date" 
      class="date-input"
    />
  </template>
  <template v-else>
    <span @click="editdate">{{ date }}</span>
  </template>
</h2>
  </div>
  <div class="undone">未完成項目：{{ undone }}</div>

    <!-- 代辦事項 -->
     <ul>
     
      <li v-for="(todo, index) in todos" :key="index" @dblclick="editTodo(index)">
        <div>
          <template v-if="editingIndex === index" >
            ✏️
      <input
        v-model="editingText"
        @keyup.enter="saveEdit(index)" 
        @blur="saveEdit(index)"
        type="text"
        class="edit-input"
      /> 
   
    </template>
    <template v-else>
          <input type="checkbox" :id="'todo-' + index" v-model="todo.completed" @change="storedTodos"  />
          <label :for="'todo-' + index">{{ todo.text }} </label>
        </template>
        </div>
        <div @click="deleteTodo(index)">❌</div>
      </li>
     </ul>
    <!-- 新增事項 -->
     <div class="newListIcon">
      <div class="add" @click="toggleInput">{{ addList }}</div>
      <template v-if="showInput">
      <input type="text" v-model="newTodo" placeholder="請輸入代辦事項"@keyup.enter="addTodo"  />
      <button @click="addTodo">新增</button>
      </template>
     
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
  margin-bottom: 10px;

}
.undone{
  font-size: 12px;
  color: #585757;
  margin-bottom: 5px;
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
li{
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5px;
  border-bottom: 1px solid #ccc;
}
.edit-input {
  border: none;
  outline: none;
  background: transparent;
 
}

.edit-input:focus {
  outline: none;
  border: none;
}

input[type="checkbox"]{
  margin-right: 5px;
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
  gap: 3px;
}
.add{
  padding:0 5px;

}
.delete{
  margin-left: 5px;
}

</style>
