<template>
  <ul>
    <Car
      v-for="car in cars" :key="car.model"
      v-bind:car="car"
    />
  </ul>
</template>
<script>
import Car from '@/components/Car.vue'

export default {
  props: ['cars'],
  components: {
    Car
  }
}
</script>
<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
