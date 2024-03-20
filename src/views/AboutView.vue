<!-- <template>
  <div>
    <p>Visited Link:
      <li>
        {{ visitedLinks[0] }}
      </li> </p>
  </div>
</template>

<script>
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
      this.visitedLinks = JSON.parse(storedLink); // Parse if stored as JSON
    }
  },
};
</script> -->

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
</script>

<style scoped>
/* Add any desired styling for the list here */
</style>
