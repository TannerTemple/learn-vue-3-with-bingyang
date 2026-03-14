<template>
  <div>
    <header>
      <!--  header content here -->
      <slot name="header"></slot>
    </header>
    <main>
      <!-- main content here -->
      <slot name="main"></slot>
    </main>
    <footer>
      
        <!-- footer content here-->
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<script setup></script>

<style scoped></style>