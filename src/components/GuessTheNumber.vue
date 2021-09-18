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

// this lets us give properties to the component
const props = defineProps({
  cheat: String // we make it possible to use a non random value
})

const elGuess = ref(null) // points to the input element
const guess = ref("") // points to the value in the input element
const msg = ref("Ich habe mir eine Zahl zwischen 1 und 100 ausgedacht!")

// if we got a value not equal 0 in the cheat property we use this value
if(props.cheat != 0) {
  var myNumber = props.cheat
} else {
  var myNumber = Math.floor(Math.random()*100)+1
}

// a little debug helper
console.log("myNumber: "+myNumber+" cheat: "+props.cheat)

// we need to use nextTickt so elGuess will be initialised
nextTick(() => { elGuess.value.focus()})

// will be called when the form gets submitted (and on "return" in the form input fields)
function submitForm() {
  console.log("Guess is "+guess.value)

  // check if the user really gave a number between 1 and 100
  if(guess.value != Math.floor(guess.value) || guess.value < 1 || guess.value > 100) {
    msg.value = "Bitte gebe eine Zahl zwischen 1 und 100 ein!"
  } else if(guess.value > myNumber) {
    msg.value = "Deine Zahl ist größer!"
  } else if(guess.value < myNumber) {
    msg.value = "Deine Zahl ist kleiner!"
  } else {
    msg.value = "Glückwunsch! Du hast meine Zahl erraten!"
  }

  // setting the focus back into the input field
  elGuess.value.focus()
  // select its contents so the user can continue
  // typing right away
  elGuess.value.select()
}
</script>

<style scoped>
input {
  max-width: 20px;
  text-align: right;
}
</style>