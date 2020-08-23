<template>
  <div id="app" class="container is-fluid">
    <ExamForm :handleSubmitExamForm="handleSubmitExamForm" :maxQuestions="examDump.length" />
    <QuestionList :questions="currentExamQuestions" />
  </div>
</template>

<script>
import ExamForm from "./components/exam/Form";
import QuestionList from "./components/exam/question/List";

import examDump from "./assets/cehv10_exam_dump.json";

export default {
  name: "App",
  components: {
    ExamForm,
    QuestionList,
  },
  data() {
    return {
      examDump: examDump,
      currentExamQuestions: [],
    };
  },
  created() {
    console.log("created");
  },
  methods: {
    handleSubmitExamForm(mode, numberOfQuestions = 720) {
      console.log("handleSubmitExamForm, mode: " + mode, " numberOfQuestions: " + numberOfQuestions);
      this.prepareQuestions(mode, numberOfQuestions);
    },
    prepareQuestions(mode, numberOfQuestions) {
      console.log("prepareQuestions");
      var currentExam = JSON.parse(JSON.stringify(this.examDump));
      currentExam = this.shuffleArray(currentExam);
      if (mode == "exam") {
        currentExam = currentExam.splice(0, numberOfQuestions);
      }
      // clean up data. This should be done before data is input into app.
      currentExam.forEach((question) => {
        question.choices = [{ a: question.a }, { b: question.b }, { c: question.c }, { d: question.d }];
        question.fullAnswer = question[question.answer.toLowerCase().trim()];
        this.$delete(question, "a");
        this.$delete(question, "b");
        this.$delete(question, "c");
        this.$delete(question, "d");
        question.choices = this.shuffleArray(question.choices);
        console.log(question.fullAnswer);
      });
      this.currentExamQuestions = currentExam;
    },
    shuffleArray(array) {
      console.log("shuffleArray");
      var counter = array.length,
        temp,
        index;
      while (counter > 0) {
        index = Math.floor(Math.random() * counter);
        counter--;
        temp = array[counter];
        array[counter] = array[index];
        array[index] = temp;
      }
      return array;
    },
  },
};
</script>

<style>
#app {
  margin-top: 20px;
}
</style>
