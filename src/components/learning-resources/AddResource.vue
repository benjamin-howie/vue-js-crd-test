<template>
  <!-- Base dialog component for invalid input -->
  <base-dialog
    @close="confirmError"
    v-if="inputIsInvalid"
    title="Invalid Input"
  >
    <!-- Default slot content for the dialog body -->
    <template #default>
      <p>Invalid Input. Please ensure all fields have been filled correctly.</p>
    </template>
    <!-- Slot for dialog actions -->
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <!-- Base card component -->
  <base-card>
    <!-- Form for input fields -->
    <form @submit.prevent="submitData" action="#">
      <!-- Fieldset for the title input -->
      <fieldset class="form-control">
        <label for="title">Title</label>
        <input type="text" required name="title" id="title" ref="titleInput" />
      </fieldset>
      <!-- Fieldset for the description input -->
      <fieldset class="form-control">
        <label for="description">Description</label>
        <textarea
          required
          name="description"
          id="description"
          cols="30"
          rows="3"
          ref="descriptionInput"
        ></textarea>
      </fieldset>
      <!-- Fieldset for the link input -->
      <fieldset class="form-control">
        <label for="link">Link</label>
        <input required type="url" name="link" id="link" ref="linkInput" />
      </fieldset>
      <div>
        <!-- Submit button -->
        <base-button type="submit">Submit</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
export default {
  inject: ['addResource'], // Inject 'addResource' method from parent
  data() {
    return {
      inputIsInvalid: false, // Flag to track invalid input
    };
  },
  methods: {
    confirmError() {
      this.inputIsInvalid = false; // Reset invalid input flag
    },
    submitData() {
      // Retrieve input values
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descriptionInput.value;
      const enteredLink = this.$refs.linkInput.value;

      // Check for empty fields
      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true; // Set invalid input flag
        return;
      }

      // Call parent method to add resource
      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
  },
};
</script>
<style scoped>
/* Styling for labels */
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

/* Styling for input and textarea elements */
input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

/* Styling for focused input and textarea elements */
input:focus,
textarea:focus {
  border-color: #3a0061; /* Purple border color */
  background-color: #f7ebff; /* Light purple background color */
}

/* Styling for form control fieldsets */
.form-control {
  margin: 1rem 0;
  border: none;
}
</style>
