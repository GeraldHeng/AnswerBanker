<template>
  <div class="content is-medium">
    <section v-for="(question, index) in questions" :key="index">
      <h5>{{ index + 1 }}. {{ question.question }}</h5>
      <div class="field">
        <div :v-if="Object.values(question.choices[0])[0] != null">
          <b-radio v-model="question.chosenChoice" :native-value="Object.values(question.choices[0])[0]">
            {{ Object.values(question.choices[0])[0] }}
          </b-radio>
        </div>
        <div :v-if="Object.values(question.choices[1])[0] != null">
          <b-radio v-model="question.chosenChoice" :native-value="Object.values(question.choices[1])[0]">
            {{ Object.values(question.choices[1])[0] }}
          </b-radio>
        </div>
        <div :v-if="Object.values(question.choices[2])[0] != null">
          <b-radio v-model="question.chosenChoice" :native-value="Object.values(question.choices[2])[0]">
            {{ Object.values(question.choices[2])[0] }}
          </b-radio>
        </div>
        <div :v-if="Object.values(question.choices[3])[0] != null">
          <b-radio v-model="question.chosenChoice" :native-value="Object.values(question.choices[3])[0]">
            {{ Object.values(question.choices[3])[0] }}
          </b-radio>
        </div>
        <div>
          <h6>
            Your Answer:
            <span
              v-bind:class="{ 'green-text': question.chosenChoice == question.fullAnswer, 'red-text': question.chosenChoice != question.fullAnswer }"
              >{{ question.chosenChoice }}</span
            >
          </h6>

          <h6>Correct Answer: {{ question.chosenChoice != null ? question.fullAnswer : "Choose your choice" }}</h6>
        </div>
      </div>

      <hr />
    </section>
  </div>
</template>

<script>
export default {
  name: "QuestionList",
  props: {
    questions: {
      type: Array,
    },
  },
  data() {
    return {
      radio: "",
    };
  },
  created() {},
  methods: {},
};
</script>

<style>
.red-text {
  color: red;
}
.green-text {
  color: green;
}
</style>
