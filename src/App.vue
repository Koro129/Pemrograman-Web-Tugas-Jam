<template>
  <div class="identity">
    <h2>Project 1</h2>
    <h3>Muhamad Ilham Yumna 5027211024</h3>
  </div>
  <Clock/>
</template>

<script>
import Clock from './components/clock.vue'
export default {
  name: 'App',
  components: {
    Clock
  }
}
</script>

<style>
body{
  background-image: url("./assets/NIER_REPLICANTV1P2_PV_Tokyo.jpg");
  background-repeat: no-repeat;
}
.identity{
  color: antiquewhite;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
