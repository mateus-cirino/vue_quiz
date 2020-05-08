<template>
  <div class="container mt">
    <div class="card">
      <div class="card-content">
        <div class="media">
          <div class="media-left"></div>
          <div class="media-content">
            <p class="title is-4">{{ pergunta.question }}</p>
            <p class="subtitle is-6">@{{ pergunta.category }}</p>
          </div>
        </div>
        <div class="content" v-for="(alternativa, index) in alternativas" :key="index">
          <b-radio
          v-model="radio"
          name="name"
          :native-value="alternativa">{{ alternativa }}</b-radio>
        </div>
        <b-button @click="verificaResposta" >Salvar</b-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['pergunta'],
  data() {
    return {
      radio: '',
    };
  },
  computed: {
    alternativas() {
      const { pergunta } = this;

      if (pergunta.incorrect_answers && pergunta.correct_answer) {
        return [...pergunta.incorrect_answers, pergunta.correct_answer].sort();
      }
      return [];
    },
  },
  methods: {
    verificaResposta() {
      if (this.radio === this.pergunta.correct_answer) {
        this.$emit('atualizarNumAcerto', true);
        this.$buefy.notification.open('Você acertou!!');
      } else {
        this.$emit('atualizarNumAcerto', false);
        this.$buefy.notification.open('Você errou!!');
      }
    },
  },

};
</script>

<style  scoped>
.mt {
  margin-top: 10px;
}
</style>
