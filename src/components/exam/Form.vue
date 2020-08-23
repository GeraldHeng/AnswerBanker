<template>
  <div class="content is-medium">
    <h4>CEH V10 EXAM</h4>
    <nav class="level">
      <!-- Left side -->
      <div class="level-left">
        <div class="level-item">
          <b-field label="Mode">
            <b-radio v-model="mode" name="name" native-value="practice" size="is-medium">
              Practice
            </b-radio>
            <b-radio v-model="mode" name="name" native-value="exam" size="is-medium">
              Exam
            </b-radio>
          </b-field>
        </div>
        <div class="level-item"></div>
      </div>
      <!-- Right side -->
      <div class="level-right">
        <div class="level-item">
            <b-field label="Number of Questions">
              <b-numberinput :disabled="mode != 'exam'" v-model="numberOfQuestions" :max="maxQuestions"></b-numberinput>
            </b-field>
        </div>
        <div class="level-item">
          <b-field label="Action">
            <button class="button" @click="onSubmitExamForm()">
              Start
            </button>
          </b-field>
        </div>
      </div>
    </nav>
    <hr />
  </div>
</template>

<script>
export default {
  name: "ExamForm",
  props: {
    handleSubmitExamForm: {
      type: Function,
    },
    maxQuestions: {
      type: Number,
    },
  },
  data() {
    return {
      mode: "practice",
      numberOfQuestions: 120,
    };
  },
  computed: {
    numberOfQuestionsValidation() {
      return this.numberOfQuestions <= 0 || this.numberOfQuestions > this.maxQuestions;
    },
  },
  methods: {
    onSubmitExamForm() {
      console.log("onSubmitExamForm");
      this.handleSubmitExamForm(this.mode, this.numberOfQuestions);
    },
  },
};
</script>
