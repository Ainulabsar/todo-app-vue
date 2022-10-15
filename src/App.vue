<template>
  <form v-on:submit.prevent="addNewTodo">
    <label class="tod">Add New Task</label>
    <input
      type="text"
      placeholder="Eg: Feed the Animal"
      class="input"
      v-model="newTodoText"
    />
    <button class="add">Add</button>
    <button @click="removeTodo" class="rmv">Remove All</button>
  </form>
  <ul class="tode">
    <li
      v-for="(todo, index) in todos"
      :key="todo"
      class="todo"
      :class="values[index].val ? 'todo' : 'noline'"
    >
      <div class="tit">{{ todo.title }}</div>
      <div class="butt">
        <button class="comp" @click="completeTodo(index)">
          <img
            src="./icons8-task-completed-30.png"
            alt="completed"
            width="20"
            height="20"
          />
        </button>
        <button class="remo" @click="todos.splice(index, 1)">
          <img src="./remove.png" alt="delete" width="20" height="20" />
        </button>
      </div>
    </li>
  </ul>
</template>

<script setup>
import { ref } from "vue";
const newTodoText = ref("");
const todos = ref([]);
const values = ref([]);
let val = ref(false);

let nextId = 1;

let nextTodoId = 1;
function addNewTodo() {
  todos.value.push({
    id: nextTodoId++,
    title: newTodoText.value,
  });
  values.value.push({
    id: nextId++,
    val: val.value,
  });

  console.log(values.value);
  newTodoText.value = "";
}
function removeTodo() {
  todos.value = [];
}
function completeTodo(i) {
  values.value[i].val = !values.value[i].val;
  console.log(values.value[i].val);
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

form {
  display: flex;
  justify-content: center;
  align-content: start;
  margin-top: 20px;
}

.add {
  width: 40px;
  margin-left: 10px;
  margin-right: 10px;
}

.tod {
  margin-right: 10px;
  width: 7em;
}

.input {
  width: 50em;
}

.rmv {
  width: 10em;
}

.tode {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-top: 20px;
  list-style-type: lower-roman;
}
.remo {
  width: 3em;
  border: none;
}

.comp {
  width: 3em;
  margin-left: 20px;
  margin-right: 20px;
  float: left;
  border: none;
}

.todo {
  text-decoration: line-through;
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  padding-right: 3rem;
  padding-left: 3rem;
}

.noline {
  text-decoration: none;
}
</style>
