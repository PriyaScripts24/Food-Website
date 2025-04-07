<template>
  <div>
    <div
      
      class="flex gap-2 flex-col justify-center items-center"
    >
      <h1 class="font-bold text-[42px]">Todo Task</h1>
      <div class="flex justify-center items-center">
        <input
          type="text"
          class="w-[400px] text-black border cursor-pointer outline-none p-2"
          placeholder="Add Task"
        />
        <button
          @click="openTodos()"
          class="w-[70px] text-black border cursor-pointer outline-none p-2"
        >
          ADD
        </button>
      </div>
    </div>
    <div class="p-6 mt-5 px-[700px]">
      <div
        v-for="task in tasks"
      :key="task"
        
        class="py-4 border-b border-gray-300"
      >
        <div class="flex gap-4">
          <input type="checkbox" />
          <button
            class="flex justify-between w-full font-bold text-left text-gray-800"
            @click="toggle(index)"
          >
            <span
              :class="{ 'text-orange-600': item.open }"
              class="md:text-[17px] text-[12px]"
              >{{ task.title }}</span
            >
            <span class="text-orange-600">{{ item.open ? "^" : ">" }}</span>
          </button>
        </div>
        <div v-if="item.open" class="mt-2 text-gray-700">
          <p
            v-for="(line, i) in item.content"
            :key="i"
            class="md:text-[14px] text-[10px]"
          >
            {{ line }}
          </p>
        </div>
      </div>
    </div>

    <div
      v-if="addTodo"
      class="bg-white w-[40%] p-10 rounded-2xl shadow-lg h-screen fixed right-0 top-0"
    >
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-lg font-semibold">Task:</h2>
        <button @click="closeTodos()" class="text-gray-500 hover:text-gray-800">
          &times;
        </button>
      </div>

      <input
        type="text"
        v-model="title"
        placeholder="Task title"
        class="w-full p-2 border rounded mb-2"
      />
      <textarea
        v-model="description"
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
          create Task
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: {
        title: "",
        description: "",
      },
      addTodo: false,
    };
  },
  methods: {
    openTodos() {
      this.addTodo = true;
      document.body.style.overflow = "hidden";
    },
    closeTodos() {
      this.addTodo = false;
      document.body.style.overflow = "";
    },
    toggle(index) {
      this.faqItems[index].open = !this.faqItems[index].open;
    },
  },
};
</script>
