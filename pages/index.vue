<template>
  <div>
    <h1>Todo</h1>
    <input v-model="value" type="text" class="border border-double p-4" />

    <button @click="addTodos()" class="border border-double p-1">Add</button>

    <div v-for="item in todos" :key="item.id" class="flex gap-3">
      <span :class="`${item.iscomplete ? 'line-through' : ''}`">{{
        item.task
      }}</span>
      <button
        @click="updatedTodo(item.id, !item.iscomplete)"
        class="border border-double p-4"
      >
        {{ item.iscomplete ? "Undone" : "done" }}
      </button>
      <button
        @click="updateTodo(item.id, item.task)"
        class="border border-double p-4"
      >
        update
      </button>
      <button @click="deleteTodo(item.id)" class="border border-double p-4">
        Delete
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      todos: [],
      value: "",
    };
  },
  mounted() {
    this.getTodos();
  },
  methods: {
    async getTodos() {
      const res = await axios.get("http://localhost:5000/todos");
      this.todos = res.data;
    },
    async addTodos() {
      if (this.value === "") {
        alert("empty");
        return;
      }
      const res = await axios.post("http://localhost:5000/todos/add", {
        task: this.value,
        completed: false,
      });
      this.value = "";
      this.getTodos();
    },
    async updatedTodo(id, iscomplete) {
      const res = await axios.put(`http://localhost:5000/todos/update/${id}`, {
        iscomplete,
      });
      this.getTodos();
    },
    async deleteTodo(id) {
      await axios.delete(`http://localhost:5000/todos/delete/${id}`);
      this.getTodos();
    },
    async updateTodo(id, value) {
      this.value = value;
    },
  },
};
</script>

<style>
.line-through {
  text-decoration: line-through;
}
</style>
