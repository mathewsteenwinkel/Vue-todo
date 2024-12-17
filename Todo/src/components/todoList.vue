<script setup>
import { ref } from 'vue';

const todos = ref([]);
const title = ref([])
const input_title = ref('')
const input_content = ref('')


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

    <form @submit.prevent="addtitle">

      <div class="body">
        <input type="text" name="category" placeholder="name your todo list" class="title" v-model="input_title" />
        <button class="submit_button">
          Submit
        </button>
      </div>
    </form>
    <form @submit.prevent="addtodo">
      <div class="body">
        <input type="text" name="category" placeholder="Create a to do item" class="input_field"
          v-model="input_content" />
        <button class="submit_button">
          Submit
        </button>
      </div>
    </form>
    <section class="todo_list">
      <section>
        <h3>Your Todo Lists:</h3>
        <ul>
          <div v-for="(item, index) in title" :key="index">
            {{ item.content }}
          </div>
        </ul>
      </section>
      <h3>Edit Todos:</h3>
      <ul class="box">
        <div v-for="(todo, index) in todos" :key="index" class="todo-item">
          <input class="items" type="text" v-model="todo.content" />
          <button class="delete" @click="removetodo(todo)">
            delete
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

.input_field {
  padding: 5px;
  margin-right: 20px;
}

.submit_button {
  font-size: 20px;
  border: 0;
  border-radius: 50%;
  background-color: rgb(255, 0, 0);
  box-shadow: 2px 5px rgb(195, 0, 0);
  ;
  height: 80px;
  width: 80px;
  cursor: pointer;
  outline: none;
}

.submit_button:active {
  transform: translateY(4px);
  box-shadow: 0 0 #021faf;
  width: 77px;
  height: 77px;
}

.submit_button:hover {
  transform: scale(1.1);
}

input {
  width: 400px;
  font-size: 30px;

}

.box {
  background-color: #021faf;
  margin: 0;
  padding: 0;
}

.todo-item {
  padding: 0;
  margin: 0;
  height: 50px;
  border: 0;

}

.todo_list {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  margin-top: 100px;
  width: 60vw;
  border-radius: 15px;
  background-color: rgb(246, 246, 231);

}
</style>
