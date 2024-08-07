<template>
  <h1>Rate Box</h1>
  <RateBox v-model="rating" :editable="true" />
  <p>Rating: {{ rating }}</p>
</template>

<script>
import { ref } from "vue";
import RateBox from "./components/RateBox.vue";

export default {
  name: "App",
  components: {
    RateBox,
  },
  setup() {
    const rating = ref(2);
    return { rating };
  },
};
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
