<script setup>
import { ref, watch, onMounted } from 'vue';

const todos = ref([]);
const name = ref('')
const input_content = ref("")


const addtodo = () => {
  if (input_content.value.trim() === "" || input_content.value === null){
    return
  }
  todos.value.push({
    content: input_content.value,
    done:false,
    editable: false,
    createdAt:new Date().getTime()
  })

}

watch(name, (newVal) => {
  localStorage.setItem("name", newVal)
})

onMounted(()=> {
  name.value = localStorage.getItem("name") || " "
})

</script>

<template>
  <div class="header">
   VUE todo
   <h1>
     Let's make a todo list in my vue todo app!
    </h1>

    <form @submit.prevent="addtodo">

      <div class="body">
        <input 
        type="text"
        name = "category"
        placeholder="Create a to do" 
        class="input_field"
        v-model="input_content"
        />
        <button class="submit_button" >
          submit
        </button>
      </div>
    </form>
  
    <section>
  <h3>Edit Todos:</h3>
  <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <input 
        class="items"
        type="text" 
        v-model="todo.content" 
        placeholder="Edit todo" 
      />
    </li>
  </ul>
</section>

  </div>

</template>

<style scoped>
.header{
  font-size: 100px;
  height: 20;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;  
}
h1{
  font-size: 40px;
}
h3{
  font-size: 25px;
}

.submit_button{
  font-size: 20px;
  border: 0;
  border-radius: 50%;
  background-color: rgba(75, 75, 255, 0.422);

  color: black;
  height: 100px;
  width: 100px;
  padding: 5px;
}

.input_field{
}

.submit_button:hover{
  transform: scale(1.2);
  transition: all 1s ease;
  background-color: rgba(75, 75, 255, 0.807);
}

input{
  width: 400px;
  font-size: 30px;

}

.items
{
  border: 0;
}
</style>
