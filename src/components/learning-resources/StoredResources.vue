<template>
  <ul>
    <!-- Iterate over resources and render LearningResource component for each resource -->
    <learning-resource
      v-for="resource in resources"
      :key="resource.id"
      :title="resource.title"
      :description="resource.description"
      :link="resource.link"
      :id="resource.id"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource.vue';

export default {
  components: { LearningResource }, // Register LearningResource component
  inject: ['resources'], // Inject 'resources' array from parent
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto; /* Center horizontally */
  max-width: 40rem;
}
</style>
