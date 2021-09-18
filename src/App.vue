<template>
  <h3>Rate meine Zahl!</h3>
  <GuessTheNumber cheat="0" />
  <!-- hr>
  <h3>Rate meine Zahl (Instanz 2 mit 12)!</h3>
  <GuessTheNumber cheat="12" /-->
</template>

<script setup>
import GuessTheNumber from './components/GuessTheNumber.vue'
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