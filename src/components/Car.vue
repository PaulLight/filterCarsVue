<template>
  <li>
    {{ car.Make }} {{ car.Model }}
  </li>
</template>

<script>
export default {
  props: ['car']
}
</script>

<style scoped>
li {
  border: 1px solid #cacaca;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
}
input {
  margin-right: 1rem;
}
</style>
