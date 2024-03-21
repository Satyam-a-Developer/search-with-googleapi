
<template>
  <div v-if="visitedLinks">
    <p>Visited Links:</p>
    <ul>
      <li v-for="link in visitedLinks" :key="link">
        {{ link }}
      </li>
    </ul>
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  data() {
    return {
      visitedLinks: null,
    };
  },
  created() {
    // Fetch data from localStorage on component creation
    const storedLink = localStorage.getItem('visitedLinks');
    if (storedLink) {
      try {
        this.visitedLinks = JSON.parse(storedLink); // Parse safely with error handling
      } catch (error) {
        console.error('Error parsing visitedLinks:', error);
        // Consider setting visitedLinks to an empty array or default value here
      }
    }
  },
};
HelloWorld
</script>

<style scoped>
/* Add any desired styling for the list here */
</style>
