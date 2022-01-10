<template>
  <div class="TotalSlot">
    <slot>Tâche</slot>
  </div>
</template>

<script>
export default {
  name: "TotalSlot"
}
</script>

<style scoped>
  .TotalSlot {
    margin: 1.5em 2px;
    font-size: 3em;
    color: red;
  }
</style>