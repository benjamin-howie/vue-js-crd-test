<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button @click="removeResource(id)" mode="flat"
          >Delete</base-button
        >
      </header>
      <p>{{ description }}</p>
      <nav><a :href="link">View Resource</a></nav>
    </base-card>
  </li>
</template>

<script>
export default {
  props: ['id', 'title', 'description', 'link'], // Declare props for the component
  inject: ['removeResource'], // Inject 'removeResource' method from parent
};
</script>

<style scoped>
/* Styling for the list item */
li {
  margin: auto; /* Center horizontally */
  max-width: 40rem;
}

/* Styling for the header */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Styling for the title */
h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

/* Styling for the navigation link */
a {
  text-decoration: none;
  color: #ce5c00;
}

/* Styling for the hover and active state of the link */
a:hover,
a:active {
  color: #c89300;
}
</style>
