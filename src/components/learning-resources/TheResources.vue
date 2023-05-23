<template>
  <!-- Base card component -->
  <base-card>
    <!-- Button to switch to 'Stored Resources' tab -->
    <base-button
      :mode="storedResourcesButtonMode"
      @click="setSelectedTab('stored-resources')"
      >Stored Resources</base-button
    >
    <!-- Button to switch to 'Add Resource' tab -->
    <base-button
      :mode="addResourceButtonMode"
      @click="setSelectedTab('add-resource')"
      >Add Resources</base-button
    >
  </base-card>
  <!-- Keep-alive component to preserve the dynamic component state -->
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue'; // Import StoredResources component
import AddResource from './AddResource.vue'; // Import AddResource component

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources', // Initially set to 'Stored Resources' tab
      storedResources: [], // Array to store the stored resources
    };
  },
  computed: {
    storedResourcesButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat'; // Determine button mode for 'Stored Resources' tab
    },
    addResourceButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat'; // Determine button mode for 'Add Resource' tab
    },
  },
  provide() {
    return {
      resources: this.storedResources, // Provide the stored resources array to child components
      addResource: this.addResource, // Provide the addResource method to child components
      removeResource: this.removeResource, // Provide the removeResource method to child components
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab; // Set the selected tab
    },
    addResource(title, description, link) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        description,
        link,
      };

      this.storedResources.unshift(newResource); // Add the new resource at the beginning of the array

      this.selectedTab = 'stored-resources'; // Switch back to the 'Stored Resources' tab
    },
    removeResource(id) {
      const resourceIndex = this.storedResources.findIndex((resource) => {
        return resource.id === id; // Find the index of the resource with the provided id
      });
      this.storedResources.splice(resourceIndex, 1); // Remove the resource from the array
    },
  },
};
</script>
