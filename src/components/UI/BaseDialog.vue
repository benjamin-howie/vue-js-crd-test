<template>
  <!-- Teleport component to move content to the <body> -->
  <teleport to="body">
    <!-- Overlay div for background, closes dialog when clicked. -->
    <div @click="$emit('close')"></div>
    <!-- Dialog component -->
    <dialog open>
      <header>
        <slot name="header">
          <!-- Default title if slot is empty -->
          <h2>{{ title }}</h2>
        </slot>
      </header>
      <section>
        <slot></slot>
      </section>
      <menu>
        <slot name="actions">
          <!-- Default close button if slot is empty -->
          <base-button @click="$emit('close')">Close</base-button>
        </slot>
      </menu>
    </dialog>
  </teleport>
</template>

<script>
export default {
  emits: ['close'], // Declare emitted event 'close'
  props: {
    title: {
      type: String,
      required: false,
    },
  },
};
</script>

<style scoped>
/* Styling for the overlay div */
div {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75); /* Semi-transparent black background */
  z-index: 10;
}

/* Styling for the dialog */
dialog {
  position: fixed;
  top: 20vh;
  left: 10%;
  width: 80%;
  z-index: 100;
  border-radius: 12px; /* Rounded corners */
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26); /* Shadow effect */
  padding: 0;
  margin: 0;
  overflow: hidden;
}

/* Styling for the header section */
header {
  background-color: #3a0061; /* Purple background */
  color: white; /* White text color */
  width: 100%;
  padding: 1rem;
}

header h2 {
  margin: 0;
}

/* Styling for the main content section */
section {
  padding: 1rem;
}

/* Styling for the actions menu section */
menu {
  padding: 1rem;
  display: flex;
  justify-content: flex-end; /* Align actions to the right */
  margin: 0;
}

/* Media query for responsive styling */
@media (min-width: 768px) {
  dialog {
    left: calc(50% - 20rem); /* Center the dialog horizontally */
    width: 40rem;
  }
}
</style>
