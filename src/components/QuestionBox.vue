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
          @input="enviarResposta"
          name="name"
          :native-value="alternativa">{{ alternativa }}</b-radio>
        </div>

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
    enviarResposta() {
      this.$emit('enviarResposta', this.radio);
    },
  },
  mounted() {
    this.radio = this.pergunta.resposta;
  },
  watch: {
    'pergunta.resposta': function (val) {
      this.radio = val;
    },
  },
};
</script>

<style  scoped>
.mt {
  margin-top: 10px;
}
</style>
