<template>
  <div class="container mt">
    <div class="card">
      <div class="card-content">
        <div class="media">
          <div class="media-left"></div>
          <div class="media-content">
            <p class="title is-4">{{ pergunta.titulo }}</p>
            <p class="subtitle is-6">@{{ pergunta.autor }}</p>
          </div>
        </div>
        <div class="content" v-for="(alternativa, index) in pergunta.alternativas" :key="index">
          <b-radio v-model="radio" name="name" :native-value="alternativa">{{ alternativa }}</b-radio>
        </div>
        <b-button @click="verificaResposta" v-bind:disabled="voto">Salvar</b-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["pergunta"],
  data() {
    return {
      radio: "",
      voto: false,
      acertou: false
    };
  },
  methods: {
    verificaResposta() {
      if (this.radio === this.pergunta.alternativaCorreta) {
        this.acertou = true;
        this.$buefy.notification.open("Você acertou!!");
      } else {
        this.$buefy.notification.open("Você errou!!");
      }
      this.voto = true;
      this.$emit("atualizarNumAcerto", this.acertou);
    }
  },

};
</script>

<style  scoped>
.mt {
  margin-top: 10px;
}
</style>