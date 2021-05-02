<template>
  <div id="app">
    <FilterCars
      :options="filterOptions"
      @filter-selected="handleFilterSelect"/>
    <CarCategory
      :cars="filteredCars"
    />
  </div>
</template>

<script>
import CarCategory from './components/CarCategory.vue'
import FilterCars from './components/FilterCars.vue'
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      cars: [],
      options: [],
      selectedFilter: ''
    }
  },
  components: {
    CarCategory,
    FilterCars
  },
  async mounted() {
    const { data } = await axios({
        method: 'get',
        url: 'https://parseapi.back4app.com/classes/Car_Model_List?count=1&limit=30',
        headers: {
          'X-Parse-Application-Id': 'hlhoNKjOvEhqzcVAJ1lxjicJLZNVv36GdbboZj3Z',
          'X-Parse-Master-Key': 'SNMJJF0CZZhTPhLDIqGhTlUNV9r60M2Z5spyWfXW',
        }
      });

    const years = [2015, 2016, 2017, 2018];

    for (let i = 0; i < 10; i++) {
      const randomItem = data.results[Math.floor(Math.random() * data.results.length)];
      randomItem.Year = years[Math.floor(Math.random() * years.length)];
    }

    console.log(data.results);

    this.cars = data.results;
  },
  computed: {
    filteredCars() {
      if (!this.selectedFilter) {
        return this.cars;
      }
      return this.cars.filter(car => car.Category === this.selectedFilter);
    },
    filterOptions() {
      const result = [];

      if (!this.cars.length) {
        return [];
      }

      this.cars.forEach(car => {
        const { Category } = car;

        if (!result.includes(Category)) {
          result.push(Category);
        }
      });

      return result;
    }
  },
  methods: {
    handleFilterSelect(filter) {
      this.selectedFilter = filter;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
