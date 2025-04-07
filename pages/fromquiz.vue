<template>
  <div>
    <div class="flex justify-center items-center">
      <div class="flex flex-col gap-6 p-5">
        <div
          class="flex flex-col bg-white w-[760px] p-5 shadow-xl border-t-8 border-t-red-700 border-transparent gap-3 border-l-6 border-l-blue-600 rounded-lg"
        >
          <div class="border-1 border-b-gray-400 border-transparent">
            <input
              v-model="title"
              type="text"
              placeholder="Untitled form"
              class="outline-none py-2 placeholder:text-[30px] text-[30px] placeholder:text-black w-full"
            />
          </div>
          <div class="border-1 border-b-gray-400 border-transparent">
            <input
              type="text"
              placeholder="Form Description"
              class="outline-none py-2 font-semibold w-full"
            />
          </div>
        </div>

        <div class="flex items-center gap-4">
          <div class="flex flex-col gap-4">
            <div
              v-for="(que, index) in questions"
              :key="index"
              class="flex flex-col bg-white w-[760px] p-5 shadow-xl gap-3"
            >
              <div class="flex justify-between items-center">
                <input
                  v-model="que.question"
                  type="text"
                  placeholder="Untitled Question"
                  class="text-[20px] outline-none w-full"
                />
                <button
                  @click="addOption(index)"
                  class="bg-blue-700 text-white px-3 py-1 rounded-lg"
                >
                  Add
                </button>
              </div>
              <div
                v-for="(option, optionIndex) in que.options"
                :key="option"
                class="flex items-center justify-between gap-3 px-5"
              >
                <input type="radio" class="w-[20px] h-[20px]" />
                <div class="py-3">
                  <input
                    v-model="questions[index].options[optionIndex]"
                    type="text"
                    placeholder="option"
                    class="placeholder:text-black placeholder:text-[20px] outline-none border-b-1 border-b-gray-600 py-3 w-[600px]"
                  />
                </div>
                <div>
                  <h1 @click="delOption(index)" class="cursor-pointer">X</h1>
                </div>
              </div>
            </div>
          </div>
          <div
            class="h-[150px] w-[30px] bg-white shadow-lg sticky top-0 flex justify-center items-start px-5 flex-col"
          >
            <h1
              @click="addQues()"
              class="text-[30px] font-black cursor-pointer"
            >
              +
            </h1>
            <h1
              @click="deleteQuiz()"
              class="text-[30px] font-black cursor-pointer"
            >
              -
            </h1>
          </div>
        </div>
        <div class="flex gap-2 flex-row justify-center items-center">
          <div class="flex justify-center items-center">
            <button
              class="bg-[#04aa6d] px-10 py-3 text-white font-semibold rounded-4xl cursor-pointer"
            >
              Send
            </button>
          </div>
          <div class="flex justify-center items-center">
            <nuxt-link to="/">
              <button
                @click="getQuizs()"
                class="bg-[#04aa6d] px-10 py-3 text-white font-semibold rounded-4xl cursor-pointer"
              >
                Quiz
              </button></nuxt-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      title: "",
      questions: [
        {
          descrpition: "",
          options: [""],
          question: "",
        },
      ],
    };
  },
  mounted() {
    // this.getQuizs();
  },
  methods: {
    addOption(index) {
      this.questions[index].options.push("");
    },
    addQues() {
      this.questions.push({
        options: [""],
        question: "",
      });
    },
    deleteQuiz() {
      this.questions.pop({
        options: [""],
        question: "",
      });
    },
    delOption(index) {
      this.questions[index].options.pop("");
    },
  },
};
</script>
