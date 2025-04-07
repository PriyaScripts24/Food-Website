<template>
  <div class="flex flex-wrap gap-5 justify-center items-center mt-10">
    <div
      v-for="quiz in quizs"
      :key="quiz"
      class="w-[350px] bg-gray-200 flex flex-col items-center p-6 gap-3 rounded-lg"
    >
      <h1 class="font-bold text-[30px] uppercase">{{ quiz.title }}</h1>
      <p class="text-[20px] text-center font-light">
        {{ quiz.questions }} Questions covering the basics of <br />
        {{ quiz.title }}
      </p>
      <div class="flex gap-2 flex-wrap justify-center">
        <NuxtLink :to="`/quizs/${quiz.id}`">
          <button
            class="bg-[#04aa6d] px-10 py-3 text-white font-semibold rounded-4xl cursor-pointer"
          >
            Start Quiz
          </button>
        </NuxtLink>
        <button
          @click="deleteQuizs(quiz.id)"
          class="bg-[#04aa6d] px-10 py-3 text-white font-semibold rounded-4xl cursor-pointer"
        >
          Delete
        </button>
        <button
          @click="updateQuizs(quiz.id)"
          class="bg-[#04aa6d] px-10 py-3 text-white font-semibold rounded-4xl cursor-pointer"
        >
          Update
        </button>
      </div>
    </div>
    <div
      @click="postQuizs()"
      class="bg-[#04aa6d] px-10 py-3 text-white font-semibold rounded-4xl cursor-pointer"
    >
      Add
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      quizs: [],
    };
  },
  methods: {
    async getQuizs() {
      try {
        const res = await axios.get("http://localhost:5000/api/quiz");
        this.quizs = res.data.quizs;
      } catch (error) {
        console.log(error);
      }
    },
    async postQuizs() {
      try {
        const res = await axios.post("http://localhost:5000/api/quiz/add", {
          title: "Untitled Quiz",
        });
        console.log(res.data);
        navigateTo(`/create/${res.data.id}`);
      } catch (err) {
        console.log(err);
      }
    },
    async deleteQuizs(id) {
      try {
        const res = await axios.delete(
          `http://localhost:5000/api/quiz/delete/${id}`
        );
        this.getQuizs();
      } catch (error) {
        console.log(error);
      }
    },
    async updateQuizs(id) {
      try {
        const res = await axios.put(
          `http://localhost:5000/api/quiz/update/${id}`
        );
        this.getQuizs();
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    this.getQuizs();
  },
};
</script>
