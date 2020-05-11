<template>
  <div id="app">
    <Header :quantidadeDePerguntasRespondidas="quantidadeDePerguntasRespondidas"
    :quantidadeDePerguntas="quantidadeDePerguntas"/>
    <QuestionBox
      :pergunta="perguntaAtual"
      @enviarResposta="enviarResposta"
      v-if="haPerguntaAtual"
    />
    <Navegacao
    @alterarPergunta="alterarPergunta"
    @salvarPergunta="salvarPergunta" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import QuestionBox from './components/QuestionBox.vue';
import Navegacao from './components/Navegacao.vue';

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Navegacao,
  },
  data() {
    return {
      perguntas: [],
      respotaTemporaria: '',
      index: 0,
      acertos: 0,
      quantidadeDePerguntas: 0,
    };
  },
  mounted() {
    fetch('https://opentdb.com/api.php?amount=10&type=multiple', {
      method: 'get',
    })
      .then((response) => response.json())
      .then((responseJson) => {
        this.perguntas = [...responseJson.results];
        this.perguntas.map((p) => [...p, { resposta: '' }]);
        this.quantidadeDePerguntas = this.perguntas.length;
      });
  },
  methods: {
    enviarResposta(resposta) {
      this.respotaTemporaria = resposta;
    },
    salvarPergunta() {
      this.perguntas[this.index].resposta = this.respotaTemporaria;
    },
    alterarPergunta(direcao) {
      if (direcao > 0) {
        if (this.haProximaPergunta) {
          this.index += 1;
        }
      } else if (this.haPerguntaAnterior) {
        this.index -= 1;
      }
    },
  },
  computed: {
    perguntaAtual() {
      return this.perguntas[this.index] || {};
    },
    haPerguntaAtual() {
      return !!this.perguntas[this.index];
    },
    haProximaPergunta() {
      return this.index < this.perguntas.length - 1;
    },
    haPerguntaAnterior() {
      return this.index > 0;
    },
    quantidadeDePerguntasRespondidas() {
      return this.perguntas.filter((p) => p.resposta !== '').length;
    },
  },
};
</script>

<style>
</style>
