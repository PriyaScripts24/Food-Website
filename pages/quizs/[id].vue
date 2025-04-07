<template>
  <div class="flex flex-col items-center gap-3">
    <div class="flex flex-col gap-4 p-5">
      <h1 class="text-[30px] font-bold">{{ quiz.title }} Quiz</h1>
      <div class="flex flex-col gap-8">
        <nuxt-link :to="`/create/${useRoute().params.id}`">
          <button>edit</button>
        </nuxt-link>
        <div
          v-for="(que, index) in questions"
          :key="index"
          class="flex flex-col gap-4"
        >
          <h3>Question {{ index + 1 }} of {{ questions.length }}</h3>
          <p>{{ que.questions }}</p>
          <div class="w-[500px]">
            <div
              v-for="option in que.options"
              :key="option"
              class="flex items-center bg-gray-100 p-3 gap-4 border-b-white border-2 border-transparent"
            >
              <input type="radio" class="w-[18px] h-[18px]" />
              <p class="text-[16px]">{{ option.options }}</p>
            </div>
          </div>
        </div>
        <button
          @click="submitForm()"
          class="bg-[#04aa6d] px-5 py-3 text-white font-semibold rounded-4xl cursor-pointer"
        >
          Submit
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      quiz: {},
      questions: [],
    };
  },

  mounted() {
    this.getQuiz();
  },
  methods: {
    async getQuiz() {
      try {
        const res = await axios.get(
          `http://localhost:5000/api/quiz/${useRoute().params.id}`
        );
        this.quiz = res.data.quiz;
        this.getQuestion();
      } catch (error) {
        console.log(error);
      }
    },
    async getQuestion() {
      try {
        const res = await axios.get(
          `http://localhost:5000/api/quiz/question/${useRoute().params.id}`
        );
        if (res.data.success === true) {
          this.questions = res.data.questions;
          if (this.questions.length === 0) {
            this.addQues();
          }
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
