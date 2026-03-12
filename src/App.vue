<template>
  <ButtonCounter></ButtonCounter>
  <!-- each button is a new instance of the same ButtonCounter class,
   when clicked, only that button counter goes up-->
  <ButtonCounter></ButtonCounter>

  <!-- kebab case also works-->
  <button-counter></button-counter>

  <hr />

  <div style="background-color: orange; padding: 5px">
    This is the root component.
    <ComponentA></ComponentA>
    <ComponentA></ComponentA>
  </div>
</template>

<script setup>
import ButtonCounter from './ButtonCounter.vue'
import ComponentA from '@/ComponentA.vue' // @ is an alias to /src
</script>

<style scoped></style>