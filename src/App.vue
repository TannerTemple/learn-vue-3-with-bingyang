<template>
  <div class="card">
    <h1 ref="title">Hello, Template Refs!</h1> <!-- need ref title here -->
    <input type="text" ref="input" />  <!-- need ref input here -->
    <button @click="printDomElements">Print DOM elements in console log</button>
    <button @click="changeTitle">Change title</button>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'

// declare a ref to hold the element reference
// the name must match template ref value
let title = ref()
const input = ref()

//^^^^ doing this above is the same as using getElementById or querySelector to get the element reference in the DOM

function printDomElements() {
  console.log(title.value)
  console.log(input.value)
}

function changeTitle() {
  title.value.innerText = 'Hello world!'
}

//allows the cursor to be active in the input when page loads
onMounted(() => {
  input.value.focus() // programmatically focus an input on component mount
})
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style>