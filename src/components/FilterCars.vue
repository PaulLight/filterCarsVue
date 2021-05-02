<template>
  <div>
    <div v-if="options.length">
      <select v-model="selected">
        <option value="">Choose</option>
        <option v-for="(option, key) in options"
                :value="option"
                :key="key"
        >
          {{ option }}
        </option>
      </select>
    </div>
    <span>Selected: {{ selected }}</span>
  </div>
</template>

<script>
export default {
  props: ['options'],
  data() {
    return {
      selected: 'Please select category'
    }
  },
  watch: {
    selected(newOption) {
      this.$emit('filter-selected', newOption);
    }
  }
}
</script>
