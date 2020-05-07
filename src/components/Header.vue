<template>
  <div>
    <b-navbar :shadow="true">
      <template slot="brand">
        <b-navbar-item :tag="home" :to="{ path: '/' }">
          <b>Quiz</b>
        </b-navbar-item>
      </template>
      <template slot="start">
        <b-navbar-item href="#">Acertos: {{acertos}}</b-navbar-item>
      </template>
    </b-navbar>
  </div>
</template>

<script>
export default {
  props: [
    'acertos'
  ]
}
</script>