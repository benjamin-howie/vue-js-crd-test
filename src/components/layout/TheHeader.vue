<template>
  <header>
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  props: ['title'],
};
</script>

<style scoped>
/* Styling for the header */
header {
  width: 100%;
  min-height: 5rem;
  background-color: #640032; /* Dark purple background */
  display: flex;
  justify-content: center;
  align-items: center;
}

header h1 {
  color: white; /* White text color */
  margin: 0;
}
</style>
