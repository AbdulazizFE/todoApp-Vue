<template>
  <div class="wrapper">
    <h1>My Todo List</h1>
    <div>
      <form class="inputFiled" @submit.prevent="create">
        <input v-model="newTodo" autocomplete="off">

        <button>Add</button>
      </form>
    </div>
    <ul class="todoList">
      <li v-for="item in todos" :key="item.id">
        <h3 :class="{ done: item.completed }" @click="completed(item)">{{ item.content }}</h3>
        <button @click="remove(item)" class="removeBtn">Delete</button>
      </li>
    </ul>
    <div class="footer">
      <button @click="selectAll()">Select All</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  setup() {
    const todos = ref([])
    const newTodo = ref('')
    function create() {
      todos.value.push({
        id: Date.now(),
        content: newTodo.value,
        completed: false
      })
      newTodo.value = ''
    }

    function remove(item) {
      todos.value.splice(todos.value.indexOf(item), 1)
    }

    function completed(item) {
      item.completed = !item.completed
    }

    function selectAll() {
      todos.value.forEach((todo) => todo.completed = true)
    }

    return {
      todos,
      newTodo,
      create,
      remove,
      completed,
      selectAll
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  width: 100%;
  height: 100vh;
  padding: 10px;
  background: #a9a9a9;
}

.wrapper {
  background: #fff;
  max-width: 400px;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
}


input {
  width: 100%;
  margin: 20px 0;
  height: 100%;
  border-radius: 3px;
  border: 1px solid #ccc;
  font-size: 17px;
  padding: 15px 5px;
  transition: all 0.3s ease;
}

form button {
  width: 100%;
  height: 100%;
  border: none;
  color: #fff;
  margin-left: 5px;
  background: #295538;
  cursor: pointer;
  padding: 5px;
  transition: all 0.3s ease;
  border-radius: 3px;
}

.todoList {
  margin: 10px -4px 10px 4px;

  max-height: 250px;
  overflow-y: auto;
}

li {
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  padding: 10px 15px;

}

.footer {
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}

.footer button {
  padding: 6px 10px;
  border-radius: 3px;
  border: none;
  color: #fff;
  background: #295538;
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}

.removeBtn {
  border: 1px solid red;
  background: none;
  padding: 5px;
  border-radius: 5px;
  margin-top: 5px;
  color: red;
  cursor: pointer;

}

.removeBtn:hover {
  background-color: red;
  color: #fff;
  transition: all 0.3s ease-in-out;
}

.item {
  cursor: pointer;
}
</style>
