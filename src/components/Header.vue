<template>
  <div>
    <b-navbar :shadow="true">
      <template slot="brand">
        <b-navbar-item :to="{ path: '/' }">
          <b>Quiz</b>
        </b-navbar-item>
      </template>
      <template slot="start">
        <b-navbar-item href="#">Perguntas respondidas:
          {{quantidadeDePerguntasRespondidas}}
          /
          {{quantidadeDePerguntas}}
          </b-navbar-item>
      </template>
    </b-navbar>
  </div>
</template>

<script>
export default {
  props: [
    'quantidadeDePerguntas',
    'quantidadeDePerguntasRespondidas',
  ],
};
</script>
