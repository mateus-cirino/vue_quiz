<template>
  <div class="container mt">
    <div class="card">
      <div class="card-content">
        <b-table
          :data="perguntas"
          :bordered="isBordered"
          :striped="isStriped"
          :narrowed="isNarrowed"
          :hoverable="isHoverable"
          :loading="isLoading"
          :focusable="isFocusable"
          :mobile-cards="hasMobileCards"
        >
          <template slot-scope="props">
            <b-table-column field="numero" label="Número" width="40" centered>{{
              perguntas.indexOf(props.row) + 1
            }}</b-table-column>

            <b-table-column field="pergunta" label="Pergunta">{{
              props.row.question
            }}</b-table-column>

            <b-table-column field="respondida" label="Respondida" centered>
              <span v-if="props.row.resposta !== ''" class="tag is-success">
                Sim
              </span>
              <span v-else class="tag is-danger">
                Não
              </span>
            </b-table-column>

            <b-table-column label="Acessar" centered>
              <span @click="acessarPergunta(perguntas.indexOf(props.row))" class="is-clickable">
                Acessar
              </span>
            </b-table-column>
          </template>
        </b-table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['perguntas'],
  data() {
    return {
      isEmpty: false,
      isBordered: false,
      isStriped: false,
      isNarrowed: false,
      isHoverable: true,
      isFocusable: false,
      isLoading: false,
      hasMobileCards: true,
    };
  },
  methods: {
    acessarPergunta(numeroDaPergunta) {
      this.$emit('voltarParaAPergunta', numeroDaPergunta);
    },
  },
};
</script>

<style  scoped>
.mt {
  margin-top: 10px;
}
.is-clickable {
  cursor: pointer;
}
</style>
