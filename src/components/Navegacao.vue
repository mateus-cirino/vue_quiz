<template>
  <div class="has-text-centered mt">
    <b-button @click="perguntaAnterior">Anterior</b-button>
    <b-button @click="salvarPergunta">Salvar</b-button>
    <b-button @click="proximaPergunta">Próximo</b-button>
    <b-button @click="atualizarResultado" class="button is-info">{{
      estadoDoBotao
    }}</b-button>
    <b-button @click="enviarResposta" class="button is-success">Enviar</b-button>
  </div>
</template>

<script>
export default {
  props: ['mostrarResultado'],
  methods: {
    perguntaAnterior() {
      this.$emit('alterarPergunta', -1);
    },
    proximaPergunta() {
      this.$emit('alterarPergunta', 1);
    },
    salvarPergunta() {
      this.$emit('salvarPergunta');
    },
    atualizarResultado() {
      this.$emit('atualizarResultado');
    },
    enviarResposta() {
      this.$emit('enviarResposta');
    },
  },
  computed: {
    estadoDoBotao() {
      if (!this.mostrarResultado) {
        return 'Status das perguntas';
      }
      return 'Voltar para as perguntas';
    },
  },
};
</script>

<style scoped>
.mt {
  margin-top: 10px;
}
</style>
