<template>
  <h1>{{ message }}</h1>

  <div class="card">
    <h1>Scenario 1: Watch a "ref(primitive value)"</h1>
    <h2>Number: {{ number }}</h2>
    <button @click="number++">Increment number by 1</button>
  </div>

  <div class="card">
    <h1>Scenario 2: Watch a property in "ref(object)"</h1>
    <h2>Name: {{ wizard1.name }}</h2>
    <h2>Wand: {{ wizard1.wand }}</h2>
    <button @click="wizard1.name = wizard1.name.toUpperCase()">
      Change name to upper case
    </button>
    <button @click="changeWizard1Wand">Change wand</button>
    <button @click="wizard1.wand.core = 'Unicorn hair'">
      Change wand core
    </button>
  </div>

  <div class="card">
    <h1>Scenario 3: Watch a "ref(object)"</h1>
    <h2>Name: {{ wizard2.name }}</h2>
    <h2>Wand: {{ wizard2.wand }}</h2>
    <button @click="wizard2.name = wizard2.name.toUpperCase()">
      Change name to upper case
    </button>
    <button @click="wizard2.wand.core = 'Phoenix feather'">
      Change wand core
    </button>
    <button @click="changeWizard">Change wizard</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

let message = ref('Hello, Watchers!')

// Scenario 1: Watch a ref(primitive value), this is a common scenario.
let number = ref(1)

const stopWatch = watch(number, (newValue, oldValue) => {
  // A callback function, called when number is changed.
  console.log(
    'Watch a ref(primitive value): number changes',
    newValue,
    oldValue
  )
  if (newValue >= 5) {
    stopWatch() //or can do unwatch(number) to stop watching number when it reaches 5 or more.
  }
}, {immediate: true}) //3rd arg: immediate: true means the callback function will be called immediately when the watch is created, 
                      //with the current value of number as newValue and undefined as oldValue.

// Scenario 2: Watch a property in a ref(object)
let wizard1 = ref({
  id: 1001,
  name: 'Harry Potter',
  house: 'Gryffindor',
  age: 17,
  wand: {
    core: 'Phoenix feather',
    wood: 'Holly'
  }
})

function changeWizard1Wand() {
  wizard1.value.wand = {
    core: 'Dragon heartstring',
    wood: 'Vine'
  }
}

//how to watch a property in a ref(object) we need use a getter function (method) to 
// return the property we want to watch, and pass it to watch
watch(
  () => wizard1.value.name,
  (newValue, oldValue) => {
    console.log(
      'Watch a property in a ref(object): wizard1 name changes',
      newValue,
      oldValue
    )
  }
)

//by default watch only tracks if the full wand value is changed (not just a part)
//so we add deep: true to watch all the properties of wand
watch(
  () => wizard1.value.wand,
  (newValue, oldValue) => {
    console.log(
      'Watch a property in a ref(object): wizard1 wand changes',
      newValue,
      oldValue
    )
  },
  { deep: true }
)

// Scenario 3: Watch a ref(object)
let wizard2 = ref({
  id: 1003,
  name: 'Ron Weasley',
  house: 'Gryffindor',
  age: 17,
  wand: {
    core: 'Unicorn hair',
    wood: 'Willow'
  }
})

function changeWizard() {
  wizard2.value = {
    id: 1002,
    name: 'Hermione Granger',
    house: 'Gryffindor',
    age: 17,
    wand: {
      core: 'Dragon heartstring',
      wood: 'Vine'
    }
  }
}

//bc of deep, triggers watch/console log, but new and old value are equal
watch(
  wizard2,
  (newValue, oldValue) => {
    console.log('Watch a ref(object): wizard2 changes', newValue, oldValue)
  },
  { deep: true }
)




// Scenario 4: Watch an array of ref(primitive value), a property of a ref(object), and a ref(object)
watch(
  [number, () => wizard1.value.name, wizard2],
  (newValue, oldValue) => {
    console.log(
      'Watch an array of ref(primitive value), a property of a ref(object), and a ref(object)'
    )
  },
  {
    deep: true
  }
)
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style>