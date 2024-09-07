<script setup>
import { ref } from 'vue';

/**
  todo item
  key: text, done 
  item.text or item['text']
  {
      text:string
      done: boolean(true/false)
  }
*/
const inputValue = ref('');
const todoList = ref([
  { text: 'vue', done: false },
  { text: 'react', done: false },
  { text: 'vercel', done: false },
]);

console.log(todoList.value);

const handleClickButton = () => {
  todoList.value.push({ text: inputValue.value, done: false });
};

const handleChange = (event) => {
  const nextValue = event.target.value;
  inputValue.value = nextValue;
};

const handleClickDeleteButton = (index) => {
  todoList.value.splice(index, 1);
};

const handleEditButton = (index) => {
  const newText = prompt("수정할 내용을 입력하세요:", todoList.value[index].text);
  if (newText !== null) {
    todoList.value[index].text = newText;
  }
};
</script>

<template>
<h4>TODO LIST</h4>

<input v-model="inputValue" />
<p>{{ inputValue }}</p>

<button @click="handleClickButton">확인</button>

<div class="todo-item" v-for="(item, index) in todoList" :key="index">
  <input type="checkbox" v-model="item.done" />
  {{ item.text }}
  
  <div>
    <button @click="handleEditButton(index)">수정</button>
    <button @click="handleClickDeleteButton(index)">삭제</button>
  </div>
</div>
</template>

.done-item(
  {
    text-decoration-line: line-through;
  }
)