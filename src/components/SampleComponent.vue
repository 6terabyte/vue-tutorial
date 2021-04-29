<template>
<div>
  <h1>samplemycomponent</h1>
  {{todo.text}}
  </div>
</template>

<script>
export default {
  name: 'SampleComponent',
  props: ['todo']
}
</script>

<style scoped>
h1 {
  background-color: magenta;
}
</style>