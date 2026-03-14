<template>
    <!-- $emit is only allowed in template-->
  <div class="blog-post">
    <p>
      {{ message }}
    </p>
    <h2>{{ id }} - {{ blogPostTitle }}</h2>
    <h4>{{ blogPostContent }}</h4> <!-- $emit with kebab case is how you pass events from child to parent -->
    <button @click="$emit('delete-blog-post', id)">Delete post</button>
    <button @click="emitDeletePostEvent(id)">Delete post</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('This is the BlogPost component.')
defineProps(['id', 'blogPostTitle', 'blogPostContent'])

// defineEmits and defineProps dont need to be imported bc they are macro functions 
// defineEmits (saved to variable) does same as $emit in template 
const emit = defineEmits(['delete-blog-post'])

function emitDeletePostEvent(id) {
  emit('delete-blog-post', id)
}
</script>

<style scoped>
.blog-post {
  background-color: aqua;
  padding: 10px;
  margin-bottom: 10px;
}
</style>