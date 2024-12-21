<script setup>
import { ref, computed } from 'vue';

const todos = ref([]);
const title = ref([]);
const input_title = ref('');
const input_content = ref('');

const showTitleInput = computed(() => title.value.length === 0);

//title logic
const addtitle = () => {
  if (input_title.value.trim() === "" || input_title.value === null) {
    return
  }
  title.value.push({
    content: input_title.value,
    done: false,
    editable: false,
  })
  input_title.value = "";

}

//todo list item logic
const addtodo = () => {
  if (input_content.value.trim() === "" || input_content.value === null) {
    return
  }
  todos.value.push({
    content: input_content.value,
    done: false,
    editable: false,
    createdAt: new Date().getTime()
  })
  input_content.value = "";
}

const removetodo = (todoToRemove) => {
  todos.value = todos.value.filter((todo) => todo !== todoToRemove);
};


</script>

<template>
  <div class="header">
    VUE todo
    <h1>
      Let's make a todo list in my vue todo app!
    </h1>
    <form v-if="showTitleInput" @submit.prevent="addtitle">
      <div class="body">
        <input 
        type="text" 
        name="category" 
        placeholder="Name your to do list" 
        class="input_field" 
        v-model="input_title" 
        
        />
        <button class="submit_button">
          Submit
        </button>
      </div>
    </form>
    <form @submit.prevent="addtodo">
      <div class="body">
        <input type="text" name="category" placeholder="Create a to do item" class="input_field"
          v-model="input_content"/>
        <button class="submit_button">
          Submit
        </button>
      </div>
    </form>
    <section class="todo_list">
      <section>
        <h3 class="title-list">Your Todo Lists:</h3>
        <ul>
          <div v-for="(item, index) in title" :key="index" class="title-show">
            {{ item.content }}
          </div>
        </ul>
      </section>
      <ul class="box">
        <div v-for="(todo, index) in todos" :key="index" class="todo-item">
          <input type="checkbox" class="checkmark"> 
          <input class="items" type="text" v-model="todo.content" />
          <button class="delete" @click="removetodo(todo)">
            Delete
          </button>
        </div>
      </ul>
    </section>

  </div>

</template>

<style scoped>
.header {
  background-color: #EEEE;
  font-size: 100px;
  height: 20;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

h1 {
  font-size: 40px;
}

h3 {
  font-size: 25px;
  margin: 0;
  padding: 0;
}

.body{
  height: 100px;
  display: flex;
  align-content: center;
  justify-content: center;
}

.submit_button {
  font-size: 14px;
  border: 0;
  border-radius: 50%;
  background-color: rgb(255, 0, 0);
  box-shadow: 2px 5px rgb(195, 0, 0);
  height: 60px;
  width: 60px;
  cursor: pointer;
  outline: none;
}

.submit_button:active {
  transform: translateY(4px);
  box-shadow: 0 0 ;
  width: 58px;
  height: 58px;
}

.submit_button:hover {
  transform: scale(1.1);
}

.box {
  margin: 0;
  padding: 0;
}

.todo-item {
  padding: 20px;
  margin: 0;
  height: 50px;
  border: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo_list {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  margin-top: 50px;
  width: 60vw;
  border-radius: 15px;
}

.delete{
  font-size: 14px;
  border: 0;
  border-radius: 50%;
  background-color: rgb(255, 0, 0);
  box-shadow: 2px 5px rgb(195, 0, 0);
  height: 50px;
  width: 50px;
  cursor: pointer;
  outline: none;
}

.input_field{
  border: 0;
  margin-right: 20px;
  height: 50px;
  width: 400px;
  font-size: 30px;
  filter: drop-shadow( 4px 5px 4px );
  padding: 10px;
  border-radius: 20px;
}

.title-show{
  display: flex;
  justify-content: center;
  font-style: italic;
}

.items{
  border: 0;
  font-size: 24px;
  background-color: transparent;
  padding: 10px;
  margin-right: 10px;
}

.title-list{
  display: flex;
  justify-content: center;
  padding: 0;
}

.checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

.checkmark {

  height: 25px;
  width: 25px;
  background-color: #eee;
}

</style>
