<template>
  <base-card>
    <base-button @click="setSelectedComponent('stored-resources')"
      :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedComponent('add-resource')"
      :mode="addResButtonMode">Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedComponent"></component>
  </keep-alive>
</template>

<script>
import storedResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    storedResources,
    AddResource,
  },
  data() {
    return {
      selectedComponent: 'stored-resources',
      storedLearningResources: [
        {
          id: 'official-guide',
          title: 'Vue Official Guide',
          description: 'The Official Vue.js Documentation',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Search and Learn Anything!',
          link: 'https://google.com'
        },
      ]
    }
  },
  provide() {
    return {
      resources: this.storedLearningResources,
      addAResource: this.addResource,
      removeResource: this.removeResource,
    }
  },
  computed: {
    storedResButtonMode() {
      return this.selectedComponent === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedComponent === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedComponent(cmp) {
      this.selectedComponent = cmp;
    },
    addResource(title, description, url) {
      const newResourceObj = {
        id: new Date().toISOString,
        title: title,
        description: description,
        link: url
      };
      this.storedLearningResources.unshift(newResourceObj);
      this.selectedComponent = 'stored-resources';
    },
    removeResource(id) {
      const resIndex = this.storedLearningResources.findIndex(res => res.id === id);
      this.storedLearningResources.splice(resIndex, 1);
    }
  },
}
</script>
