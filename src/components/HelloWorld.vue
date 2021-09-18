<template>
  <span>{{ msg }}</span>
  <br/>
  <br/>
  <form @submit.prevent="submitForm">
  <label>Was denkst Du ist meine Zahl? <input v-model="guess" ref="elGuess" type="text" name="guess"></label>
  </form>
</template>

<script setup>
import { reactive, ref, toRefs } from 'vue'

const props = defineProps({
  cheat: String
})

const elGuess = ref()
const guess = ref()
const msg = ref("Ich habe mir eine Zahl zwischen 1 und 100 ausgedacht!")

if(props.cheat != 0) {
  var myNumber = props.cheat
} else {
  var myNumber = Math.floor(Math.random()*100)+1
}

function submitForm() {
  console.log("Guess is "+guess.value+" myNumber: "+myNumber+" cheat: "+props.cheat)
  elGuess.value.focus()
  elGuess.value.select()
}

</script>

<style scoped>
a {
  color: #42b983;
}
</style>