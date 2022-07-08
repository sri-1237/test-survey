<template>
  <div class="test-survey-builder">
    <h2 class="text-center">Vue Survey Builder Demo</h2>
    <hr/>
    <QuestionsView :questions="questionsList" :readOnly="true" />
    <div v-if="addQuestion">
      <SurveyBuilder :options="sampleQuestion" @add-update-question="updateQuestionsList"/>
    </div>
    <div class="pt-10">
      <button type="button" class="add_another_btn br-25" v-on:click="addNewQuestion()">Add question</button>
    </div>
  </div>
</template>

<script>
import SurveyBuilder from './components/SurveyBuilder.vue';
import QuestionsView from './components/QuestionView.vue';
import sampleQuestionObj from './components/survey-builder.json';

export default {
  name: 'TestSurveyBuilder',
  data() {
    return {
      questionsList: [],
      addQuestion: false,
    };
  },
  mounted() {
    // this.$root.$on('add-update-question', q => {
    //   this.updateQuestionsList(q);
    // });
  },
  components: { SurveyBuilder, QuestionsView },
  methods: {
    updateQuestionsList(q) {
      console.log("qqq..",q.question);
      var question = q.question;
      const questionIndex = this.questionsList.findIndex(x => x.id === question.id);
      console.log("q index..",questionIndex);
      if (questionIndex >= 0) {
        this.questionsList.splice(questionIndex, 1, question);
      } else {
        this.questionsList.push(JSON.parse(JSON.stringify(question)));
      }
      this.addQuestion = false;
      this.$emit('selected-question', null);
      console.log("q list", JSON.stringify(this.questionsList))
      window.console.log(question, this.addQuestion, this.questionsList);
    },
    addNewQuestion() {
      this.sampleQuestion = JSON.parse(JSON.stringify(sampleQuestionObj));
      console.log("111111",this.sampleQuestion)
      this.addQuestion = true;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.add_another_btn {
  font-size: 14px;
  background-color: transparent;
  border-color: #4c8ce4;
  color: #4c8ce4;
  padding: 8px;
  cursor: pointer;
}
.text-center {
  text-align: center;
}
</style>

