<template>
  <!-- Button component -->
  <button :type="type" :class="mode">
    <!-- Insert content within the button -->
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['type', 'mode'], // Declare props for the component
};
</script>

<style scoped>
/* Styling for the button */
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
}

/* Hover and active state styles for the button */
button:hover,
button:active {
  background-color: #270041;
  border-color: #270041;
}

/* Styling for the "flat" mode of the button */
.flat {
  background-color: transparent;
  color: #3a0061;
  border: none;
}

/* Hover and active state styles for the "flat" mode */
.flat:hover,
.flat:active {
  background-color: #edd2ff;
}
</style>
