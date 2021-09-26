<template>
  <div id="app">
    <EMICalculator />
    <router-view />
  </div>
</template>
<script>
import EMICalculator from "@/components/EMICalculator";

export default {
  name: "App",
  components: {
    EMICalculator,
  },
};
</script>

<style>
#app {
  background-color: yellow;
  margin: 0px;
}
