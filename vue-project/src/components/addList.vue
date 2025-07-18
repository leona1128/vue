<script setup>
import { ref } from 'vue'

const emit = defineEmits(['submit', 'close'])
const showAddList = ref(false)
const newNoteColor = ref('#ffffff')
const title = ref('');
function addNote(){
    showAddList.value = true;
}
function closeAddList() {
    showAddList.value = false;
    title.value = '';
}
function submitNote(){
    console.log('按了新增按鈕！') 
    if (title.value.trim() !== '') {
        console.log('要發送的資料：', { title: title.value, color: newNoteColor.value }) 
        emit('addlist', {
            title: title.value.trim(),
            color: newNoteColor.value
        })
        closeAddList()
    }
}

</script>

<template>
<div class="addList">
    <button class='addBtn' type="button" @click="addNote">➕</button>
  <div class="addList_container" v-if="showAddList">
    <div class="addList_header">
      <input
        v-model="title"
        @keyup.enter="saveAddEdit(index)"  type="text" placeholder='標題'>{{title}}</input>
      <button @click="closeAddList">❌</button>
    </div>
      <label for="color">選擇顏色:</label>
      <input type="color" v-model="newNoteColor" id="color"/>
      <button type="button" @click="submitNote">新增</button>
    </div>
  </div>
</template>

<style scoped>
.addList{
    position: fixed;
    bottom: 10px;
    left: 10px;
    z-index: 1000;
}
.addBtn{
font-size: 50px;
bottom: 10px;
left: 10px;

}

button {
background-color: #f0f0f000;
  border: none;
  cursor: pointer;
}
.addList_container{
    position: absolute;
    bottom: 100px;
    left: 50px;
    background-color: #7fc7ff59;
    width: 300px;
    height: 100px;

}
.addList_header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background-color: #f0f0f0;
    border-bottom: 1px solid #ccc;
}

</style>
