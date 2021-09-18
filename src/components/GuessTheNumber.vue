<template>
  <span>{{ msg }}</span>
  <br/>
  <br/>
  <form @submit.prevent="submitForm">
  <label>Was denkst Du ist meine Zahl? <input v-model="guess" ref="elGuess" type="text"></label>
  </form>
</template>

<script setup>
import { ref, nextTick } from 'vue'

const props = defineProps({
  cheat: String
})

const elGuess = ref(null)
const guess = ref("")
const msg = ref("Ich habe mir eine Zahl zwischen 1 und 100 ausgedacht!")

if(props.cheat != 0) {
  var myNumber = props.cheat
} else {
  var myNumber = Math.floor(Math.random()*100)+1
}

console.log("myNumber: "+myNumber+" cheat: "+props.cheat)

nextTick(() => { elGuess.value.focus()})

function submitForm() {
  console.log("Guess is "+guess.value)
  if(guess.value != Math.floor(guess.value) || guess.value < 1 || guess.value > 100) {
    msg.value = "Bitte gebe eine Zahl zwischen 1 und 100 ein!"
  } else if(guess.value > myNumber) {
    msg.value = "Deine Zahl ist größer!"
  } else if(guess.value < myNumber) {
    msg.value = "Deine Zahl ist kleiner!"
  } else {
    msg.value = "Glückwunsch! Du hast meine Zahl erraten!"
  }

  elGuess.value.focus()
  elGuess.value.select()
}

</script>

<style scoped>
input {
  max-width: 20px;
  text-align: right;
}
a {
  color: #42b983;
}
</style>