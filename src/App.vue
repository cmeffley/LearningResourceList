<template>
  <stored-resources :resources="storedLearningResources"></stored-resources>
</template>

<script>
import storedResources from './components/learning-resources/StoredResources.vue';

export default {
  components: {
    storedResources,
  },
  data() {
    return {
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
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>
