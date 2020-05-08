<template>
  <div id="app">
    <Header :acertos="acertos" />
    <QuestionBox :pergunta="perguntaAtual" @atualizarNumAcerto="atualizarNumAcerto" v-if="haPerguntaAtual" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      perguntas: [],
      index: 0,
      acertos: 0
    };
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&type=multiple", {
      method: "get"
    })
      .then(response => {
        return response.json();
      })
      .then(responseJson => {
        this.perguntas = responseJson.results;
      });
  },
  methods: {
    atualizarNumAcerto(acerto) {
      if (acerto) {
        this.acertos++;
      }
      this.index++;
    }
  },
  computed: {
    perguntaAtual() {
      return this.perguntas[this.index] || {};
    },
    haPerguntaAtual() {
      return !!this.perguntas[this.index];
    }
  }
};
</script>

<style>
</style>
