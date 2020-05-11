<template>
  <div class="has-text-centered mt">
    <b-button @click="perguntaAnterior">Anterior</b-button>
    <b-button @click="salvarPergunta">Salvar</b-button>
    <b-button @click="proximaPergunta">Próximo</b-button>
  </div>
</template>

<script>
export default {
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
  },
};
</script>

<style  scoped>
.mt {
  margin-top: 10px;
}
</style>
