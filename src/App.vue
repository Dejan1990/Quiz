<template>
  <div id="app" class="containers">
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Header 
            :totalQuestion="questions.length"
            :countQuestion="questions.length ? index + 1 : index"
            :countCorrect="countCorrect"
          />
        </b-col>
      </b-row>
    </b-container>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Menu 
            :fetchApi="fetchApi"
            v-on:resetMenu="resetQuestion"
          />
        </b-col>
        <b-col sm="6" offset="3" v-if="selectedOption && !questions.length">
          <Loading />
        </b-col>
        <b-col sm="6" offset="3" v-else>
          <QuestionBox 
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :selectedOption="selectedOption"
            :next="next"
            :increment="increment"
            :resetQuestion="resetQuestion"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Menu from './components/Menu.vue'
import Loading from './components/Loading.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    Menu,
    Loading,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      selectedOption: '',
      index: 0,
      countCorrect: 0,
      api: 'https://opentdb.com/api.php?amount=10&type=multiple'
    }
  },
  methods: {
    resetQuestion() {
      this.questions = [];
      this.countCorrect = 0;
      this.index = 0;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.countCorrect++;
      }
    },
    next() {
      this.index++;
    },
    fetchApi(api, name) {
      this.selectedOption = name;
      if (api) {
        this.api = api;
        this.loadData();
      }
    },
    loadData() {
      fetch(this.api, { method: 'get' })
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.questions = jsonData.results;
      })
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

div {
  text-align: center;
}
</style>
