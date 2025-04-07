<template>
  <div>
    <div class="flex justify-center items-center">
      <div class="flex flex-col gap-6 p-5">
        <div
          class="flex flex-col bg-white w-[760px] p-5 shadow-xl border-t-8 border-t-red-700 border-transparent gap-3 border-l-6 border-l-blue-600 rounded-lg"
        >
          <div class="border-1 border-b-gray-400 border-transparent">
            <div class="flex">
              <input
                v-model="quiz.title"
                type="text"
                placeholder="Untitled form"
                class="outline-none py-2 placeholder:text-[30px] text-[30px] placeholder:text-black w-full"
              />
              <button @click="updateQuiz()">update</button>
            </div>
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
                  v-model="que.questions"
                  type="text"
                  placeholder="Untitled Question"
                  class="text-[20px] outline-none w-full"
                />
                <div class="flex gap-2">
                  <button @click="updateQues(index)">update</button>
                  <div>
                    <h1 @click="deleteQues(que.id)" class="cursor-pointer">
                      X
                    </h1>
                  </div>
                </div>
              </div>
              <button
                @click="addOption(que.id)"
                class="bg-blue-700 text-white px-3 py-1 rounded-lg"
              >
                Add
              </button>
              <div
                v-for="(option, optionIndex) in que.options"
                :key="option"
                class="flex items-center justify-between gap-3 px-5"
              >
                <input type="radio" class="w-[20px] h-[20px]" />
                <div class="py-3 flex gap-2">
                  <input
                    v-model="questions[index].options[optionIndex].options"
                    type="text"
                    placeholder="option"
                    class="placeholder:text-black placeholder:text-[20px] outline-none border-b-1 border-b-gray-600 py-3 w-[600px]"
                  />
                  <button
                    @click="
                      updateOption(
                        questions[index].options[optionIndex].id,
                        index,
                        optionIndex
                      )
                    "
                  >
                    update
                  </button>
                </div>
                <div>
                  <h1
                    @click="delOption(questions[index].options[optionIndex].id)"
                    class="cursor-pointer"
                  >
                    X
                  </h1>
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
      quiz: {
        title: "",
      },
      questions: [],
    };
  },
  mounted() {
    this.getQuiz();
    this.getQuestion();
  },
  methods: {
    async getQuiz() {
      try {
        const res = await axios.get(
          `http://localhost:5000/api/quiz/${useRoute().params.id}`
        );
        this.quiz = res.data.quiz;
      } catch (error) {
        console.log(error);
      }
    },

    async updateQuiz() {
      try {
        const res = await axios.put(
          `http://localhost:5000/api/quiz/update/${useRoute().params.id}`,
          {
            title: this.quiz.title,
          }
        );
        this.quiz = res.data.quiz;
      } catch (error) {
        console.log(error);
      }
    },

    async addQues() {
      try {
        const res = await axios.post(
          "http://localhost:5000/api/quiz/question/add",
          {
            questions: "enter your question",
            quizId: `${useRoute().params.id}`,
            answer: "",
          }
        );
        if (res.data.success === true) {
          this.addOption(res.data.id);
        }

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
    async updateQues(index) {
      try {
        const res = await axios.put(
          `http://localhost:5000/api/quiz/question/update/${this.questions[index].id}`,
          {
            questions: this.questions[index].questions,
            quizId: useRoute().params.id,
          }
        );
        // this.questions = res.data.questions;
        this.getQuestion();
      } catch (error) {
        console.log(error);
      }
    },
    async addOption(quesId) {
      try {
        const res = await axios.post(
          "http://localhost:5000/api/quiz/option/add",
          {
            options: "option 1",
            questionId: quesId,
          }
        );

        this.getQuestion();
      } catch (error) {
        console.log(error);
      }
    },
    async updateOption(id, index, optionIndex) {
      try {
        const res = await axios.put(
          `http://localhost:5000/api/quiz/option/update/${id}`,
          {
            options: this.questions[index].options[optionIndex].options,
            questionId: this.questions[index].id,
          }
        );
        this.getQuestion();
      } catch (error) {
        console.log(error);
      }
    },

    deleteQuiz() {
      this.questions.pop({
        options: [""],
        question: "",
      });
    },
    async delOption(id) {
      try {
        const res = await axios.delete(
          `http://localhost:5000/api/quiz/option/delete/${id}`
        );
        this.getQuestion();
      } catch (error) {
        console.log(error);
      }
    },
    async deleteQues(id) {
      try {
        const res = await axios.delete(
          `http://localhost:5000/api/quiz/question/delete/${id}`
        );
        // this.questions = res.data.questions;
        this.getQuestion();
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
