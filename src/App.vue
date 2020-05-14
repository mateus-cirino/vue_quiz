<template>
  <div id="app">
    <Header :quantidadeDePerguntasRespondidas="quantidadeDePerguntasRespondidas"
    :quantidadeDePerguntas="quantidadeDePerguntas"/>
    <Resultados
    :perguntas="perguntas"
    @voltarParaAPergunta="voltarParaAPergunta"
    v-if="mostrarResultado" />
    <QuestionBox
      :pergunta="perguntaAtual"
      @enviarResposta="enviarResposta"
      v-if="!mostrarResultado"
    />
    <Navegacao
    :mostrarResultado="mostrarResultado"
    @enviarResposta="finalizar"
    @atualizarResultado="atualizarResultado"
    @alterarPergunta="alterarPergunta"
    @salvarPergunta="salvarPergunta" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import QuestionBox from './components/QuestionBox.vue';
import Navegacao from './components/Navegacao.vue';
import Resultados from './components/Resultados.vue';

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Navegacao,
    Resultados,
  },
  data() {
    return {
      perguntas: [],
      respotaTemporaria: '',
      index: 0,
      acertos: 0,
      quantidadeDePerguntas: 0,
      mostrarResultado: false,
    };
  },
  mounted() {
    fetch('https://opentdb.com/api.php?amount=10&type=multiple', {
      method: 'get',
    })
      .then((response) => response.json())
      .then((responseJson) => {
        this.perguntas = responseJson.results.map((p) => ({ ...p, resposta: '' }));
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
    atualizarResultado() {
      this.mostrarResultado = !this.mostrarResultado;
    },
    voltarParaAPergunta(numeroDaPergunta) {
      this.index = numeroDaPergunta;
      this.atualizarResultado();
    },
    finalizar() {
      const pontuacao = this.perguntas.reduce((inicio, pergunta) => {
        if (pergunta.resposta !== '' && pergunta.correct_answer === pergunta.resposta) {
          return inicio + 1;
        }
        return inicio;
      }, 0);
      this.alert(pontuacao);
    },
    alert(pontuacao) {
      this.$buefy.dialog.alert({
        title: 'Resultado final',
        message: `Você acertou ${pontuacao} questões`,
        type: 'is-success',
      });
    },
  },
  computed: {
    perguntaAtual() {
      return this.perguntas[this.index] || {};
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
