<!-- able to add code at certain times in a components lifecycle -->
<template>
  <h1>{{ message }}</h1>
  <div class="card">
    <h2 ref="title">This is the App component.</h2>
    <h2>Number: {{ number }}</h2>
    <button @click="number++">Increment number by one</button>
    <button @click="isShow = !isShow">Toggle component1</button>
    <Component1 v-if="isShow"></Component1> <!-- think of this line as a placeholder for the html code in componenet1.vue-->
  </div>
</template>

<script setup>
import {
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  watch
} from 'vue'

import Component1 from './Component1.vue'

let message = ref('Hello, Lifecycle Hooks!')

let number = ref(1) //number is a reactive data (1 here)
let title = ref(null)

let isShow = ref(true)

console.log('App component is setup.') //from code along

onBeforeMount(() => {
  console.log('App component is before mount.')
  console.log(number.value) // The ref data works.
  console.log(title.value) // Since the component has not yet been mounted, you won't have access to the component's template or DOM elements within onBeforeMount.
})

//a component is considered mounted after:
  // 1. all of its synchronous child components have been mounted
  // 2. its own DOM tree has been created and inserted into the parent container

onMounted(() => { //parent is last to be mounted 
  console.log('App component is mounted.')
  console.log(title.value) // This works once the component is mounted.
})

//on Before Updarte and on Updated are only called when elements in the DOM are changed
onBeforeUpdate(() => {    //used to capture info about current DOM before it is changed
  console.log('App component is before update.')
})
onUpdated(() => {
  console.log('App component is updated.')
})
onBeforeUnmount(() => {
  console.log('App component is before unmount.')
})
onUnmounted(() => {
  console.log('App component is unmounted.')
})

//watchers get called before hook functions 
// data changed first, then the DOM tree
watch(number, () => {
  console.log('number changes!')
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


