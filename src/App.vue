<template>
  <div id="app">
    <Header :acertos="acertos" />
    <QuestionBox :pergunta="pergunta" v-for="(pergunta, index) in perguntas" :key="index" @atualizarNumAcerto="atualizarNumAcerto" />
  </div>
</template>

<script>

import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      perguntas: [
      {
          titulo: "Qual o maior país da América Latina",
          autor: "mateus-cirino",
          alternativas: ["Brasil", "Argentina", "Uruguai"],
          alternativaCorreta: "Brasil"
      },
      {
          titulo: "Quem é o namorado da Larissa",
          autor: "mateus-cirino",
          alternativas: ["Mateus", "Geraldo", "Felipe"],
          alternativaCorreta: "Mateus"
      }
      ],
      acertos: 0
    }
  },
  methods: {
    atualizarNumAcerto(acerto) {
      if(acerto) {
        this.acertos++;
      }
    }
  }
}
</script>

<style>

</style>
