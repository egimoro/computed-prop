<script>
let id = 0;

export default {
  data() {
    return {
      newTodo: "",
      hideCompleted: false,
      todos: [
        { id: id++, text: "Learn HTML", done: true },
        { id: id++, text: "Learn JavaScript", done: true },
        { id: id++, text: "Learn Vue", done: false },
      ],
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos;
    },
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: id++,
        text: this.newTodo,
        done: false,
      });
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
  },
};
</script>

<template>
  <div>
    <form class="submit" @submit.prevent="addTodo">
      <input v-model="newTodo" />
      <button class="add">Add Todo</button>
    </form>
  </div>
  <div class="box">
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="removeTodo(todo)">X</button>
      </li>
    </ul>
  </div>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleded ? "Show all" : "Hide completed" }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}

body {
  background: #f0ebf4;
}
.box {
  display: flex;
  background-color: #cfd5e6;
  border: 2px solid green;
  max-width: 300px;
  margin: 20px;
  padding: 50px;
  border-radius: 15px;
  outline-style: outset;
  outline-width: medium;
  outline-color: cornflowerblue;
}

.box > div {
  background-color: #f1f1f1;
  margin: 10px;
  padding: 20px;
  font-size: 30px;
}

.submit {
  width: 320px;
  padding: 20px;
  border: 5px solid #c4dbf6;
  margin: 30px;
}

.add {
  border-style: inset;
  border: 2px solid #1f5621;
  border-radius: 5px;
  background-color: #8aa6c9;
  height: 30px;
  width: 80px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  margin-left: 10px;
}
</style>
