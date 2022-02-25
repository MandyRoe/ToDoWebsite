<template>
  <div class="card">
    <h3>{{ todo.title }}</h3>
    <p>{{ todo.description }}</p>
    <pre>{{ todo }}</pre>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Todo",
  props: {
    todo: {},
  },
};
</script>

<style scoped>
.card {
  border: 1px solid black;
  margin-bottom: 20px;
  padding: 10px;
  border-radius: 15px;
}
</style>