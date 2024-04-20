<template>
  <HomePage :person="person" :count="count" @plus="handlePlus" @minus="handleMinus"/>
</template>

<script>
import HomePage from './pages/Home.vue'

export default {
  name: 'App',
  components: {
    HomePage
  },
  data() {
    return {
      count: 0,
      person: {
        fullname: "John Doe",
        country: "Spain",
        age: 17
      }
    };
  },
  methods: {
    handlePlus() {
      this.count++;
    },
    handleMinus() {
      this.count--;
    },
  },
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
