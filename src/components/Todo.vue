<template>
  <div :class="todo.statut">
    <h1>{{todo.nom}}</h1>
    <p>{{todo.desc}}</p>
    <button v-show="todo.statut === 'waiting'" @click="goStarted">Démarrer</button>
    <button v-show="todo.statut === 'started'" @click="goEnded">Terminer</button>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: Object
  },
  methods: {
    goStarted() {
      this.$emit('started', this.todo.id)
    },
    goEnded() {
      this.$emit('ended', this.todo.id)
    },
  }
}
</script>

<style scoped>
  div {
    border: 1px solid silver;
  }
  .waiting {
    background-color: red;
  }
  .ended {
    background-color: green;
  }
  .started {
    background-color: orange;
  }
</style>