<!-- <template>
  <div class="max-w-lg mx-auto p-6 bg-white shadow-lg rounded-lg">
    <h2 class="text-2xl font-bold mb-4">Todo Task </h2>

    <div class="flex mb-4">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Add a new task..."
        class="flex-grow p-2 border rounded-l-md focus:outline-none focus:ring"
      />
      <button
        @click="addTask"
        class="bg-blue-500 text-white px-4 py-2 rounded-r-md"
      >
        Add
      </button>
    </div>

    <ul>
      <li
        v-for="task in tasks"
        :key="task.id"
        class="flex items-center justify-between bg-gray-100 p-3 rounded-md mb-2"
      >
        <div class="flex items-center">
          <input
            type="checkbox"
            v-model="task.completed"
            @change="toggleTask(task)"
            class="mr-2"
          />
          <span :class="{ 'line-through text-gray-500': task.completed }">{{
            task.title
          }}</span>
        </div>
        <button @click="deleteTask(task.id)" class="text-red-500">✖</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default defineNuxtComponent({
  setup() {
    const tasks = ref([
      { id: 1, title: "Research content ideas", completed: false },
      { id: 2, title: "Create a database of guest authors", completed: false },
      { id: 3, title: "Renew driver's license", completed: false },
      { id: 4, title: "Consult accountant", completed: false },
      { id: 5, title: "Print business card", completed: false },
    ]);

    const newTask = ref("");

    const addTask = () => {
      if (newTask.value.trim()) {
        tasks.value.push({
          id: Date.now(),
          title: newTask.value,
          completed: false,
        });
        newTask.value = "";
      }
    };

    const toggleTask = (task) => {
      task.completed = !task.completed;
    };

    const deleteTask = (taskId) => {
      tasks.value = tasks.value.filter((task) => task.id !== taskId);
    };

    return { tasks, newTask, addTask, toggleTask, deleteTask };
  },
});
</script>

<style>
body {
  background-color: #f3f4f6;
  font-family: "Arial", sans-serif;
}
</style> -->

<!-- <template>
  <div class="p-10 flex flex-col gap-10 items-center">
    <div class="flex items-center gap-5">
      <h1 class="text-[50px] font-semibold">Today</h1>
      <div
        class="border border-gray-600 w-[50px] h-[70px] flex justify-center items-center rounded"
      >
        <h1 class="text-3xl font-bold">5</h1>
      </div>
    </div>
    <div>
      <div @click="open()" class="w-[500px]">
        <input
          type="text"
          placeholder="+ Add Task"
          class="border border-slate-400 w-full h-[50px] rounded px-3 text-2xl font-semibold outline-none"
        />
      </div>
      <div class="flex items-center gap-5 border border-gray-600">
        <input type="checkbox" />
        <p class="w-full h-[50px]"></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script> -->

<!-- <template>
  <div
    class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
  >
    <div class="bg-white w-96 p-6 rounded-2xl shadow-lg">
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-lg font-semibold">Task:</h2>
        <button
          @click="closeModal"
          class="text-gray-500 hover:text-gray-800 w-[20px] h-[20px]"
        >
          x
        </button>
      </div>

      <input
        type="text"
        v-model="taskTitle"
        placeholder="Task title"
        class="w-full p-2 border rounded mb-2"
      />
      <textarea
        v-model="taskDescription"
        placeholder="Description"
        class="w-full p-2 border rounded mb-2"
      ></textarea>

      <label class="block mb-2">List</label>
      <select v-model="taskList" class="w-full p-2 border rounded mb-2">
        <option>Personal</option>
        <option>Work</option>
        <option>Others</option>
      </select>

      <label class="block mb-2">Due date</label>
      <input
        type="date"
        v-model="dueDate"
        class="w-full p-2 border rounded mb-2"
      />

      <div class="mb-2">
        <label class="block mb-2">Tags</label>
        <div class="flex gap-2 items-center">
          <span
            v-for="tag in tags"
            :key="tag"
            class="bg-blue-100 text-blue-700 px-2 py-1 rounded"
            >{{ tag }}</span
          >
          <button
            @click="addTag"
            class="text-gray-500 px-2 py-1 border rounded"
          >
            + Add Tag
          </button>
        </div>
      </div>

      <div class="mb-2">
        <label class="block mb-2">Subtasks:</label>
        <button
          @click="addSubtask"
          class="text-gray-600 flex items-center gap-1 mb-2"
        >
          + Add New Subtask
        </button>
        <div
          v-for="(subtask, index) in subtasks"
          :key="index"
          class="flex items-center gap-2 mb-1"
        >
          <input type="checkbox" v-model="subtask.completed" />
          <input
            type="text"
            v-model="subtask.text"
            class="w-full p-1 border rounded"
          />
        </div>
      </div>

      <div class="flex justify-between mt-4">
        <button class="bg-gray-200 px-4 py-2 rounded">Delete Task</button>
        <button class="bg-yellow-500 text-white px-4 py-2 rounded">
          Save changes
        </button>
      </div>
    </div>
  </div>
</template>

<script setup> -->
<!-- import { ref } from "vue";

const taskTitle = ref("Renew driver’s license");
const taskDescription = ref("");
const taskList = ref("Personal");
const dueDate = ref("2022-03-11");
const tags = ref(["Tag 1"]);
const subtasks = ref([{ text: "Subtask", completed: false }]);

const addTag = () => {
  tags.value.push(`Tag ${tags.value.length + 1}`);
};

const addSubtask = () => {
  subtasks.value.push({ text: "", completed: false });
};

const closeModal = () => {
  console.log("Modal closed");
};
</script> -->

<template>
  <div>
    <div class="task-app">
      <h1>Task Manager</h1>
      <input
        v-model="newTask"
        placeholder="Add new task"
        @keyup.enter="addTask"
      />
      <button @click="addTask">Add Task</button>
      <ul>
        <li v-for="task in tasks" :key="task.id">
          <span>{{ task.title }}</span>
          <button @click="deleteTask(task.id)">Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: "",
      selectedTask: null,
    };
  },
  async mounted() {
    await this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await fetch("http://localhost:5000/tasks");
        this.tasks = await response.json();
      } catch (error) {
        console.error("Error fetching tasks:", error);
      }
    },
    async addTask() {
      if (!this.newTask) return;
      try {
        const response = await fetch("http://localhost:5000/tasks", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ title: this.newTask, completed: false }),
        });
        const task = await response.json();
        this.tasks.push(task);
        this.newTask = "";
      } catch (error) {
        console.error("Error adding task:", error);
      }
    },
    async deleteTask(id) {
      try {
        await fetch(`http://localhost:5000/tasks/${id}`, { method: "DELETE" });
        this.tasks = this.tasks.filter((task) => task.id !== id);
      } catch (error) {
        console.error("Error deleting task:", error);
      }
    },
  },
};
</script>
