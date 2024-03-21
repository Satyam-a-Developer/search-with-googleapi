<template>
  <div>
    <div>
      <input v-model="inputValue" type="text" placeholder="Enter text" />
      <button @click="fetchData">Fetch Data</button>
    </div>
    <div v-if="fetchedData">
      <ul>
        <li v-for="item in fetchedData" :key="item.link">
          <a
            :href="item.link"
            @click="handleClick"
            :style="{ backgroundColor: backgroundColor }"
            target="_blank"
          >{{ item.title }}</a>
          <img
            v-if="item.pagemap && item.pagemap.cse_image"
            :src="item.pagemap.cse_image[0].src"
            :alt="item.title"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
a:visited {
  color: red;
}

input {
  border: 10px solid rgb(0, 0, 0);
  width: 80vw;
  border-radius: 20px;
  font-size: 50px;
  height: 50px;
  padding: 10px;
}

button {
  padding: 40px;
  border: none;
  font-size: 40px;
  border-radius: 20px;
  margin: 70px;
}

div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100vw;
}

li a {
  color: white;
  width: 100vw;
  height: 300px; /* Adjust height as needed */
}

a:hover {
  color: rgb(255, 0, 0);
  text-decoration: none;
}

a {
  text-decoration: none;
}

ul {
  list-style: none;
  display: flex;
  color: aqua;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: scroll;
  flex-wrap: nowrap;
}

img {
  display: flex;
  padding: 30px;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 300px;
  height: 300px; /* Adjust height as needed */
}
</style>

<script>
export default {
  data() {
    return {
      backgroundColor: 'black', // Initial background color
      visitedLinks: JSON.parse(localStorage.getItem('visitedLinks')) || [],
      inputValue: '',
      trackVisitedLinks:null,
      fetchedData: null,
    };
  },
  methods: {
    handleClick() {
      this.backgroundColor = 'black'; // Change background color on click
      const currentLink = this.$el.querySelector('a').href; // Get the link

      // Check if link is already visited
      if (!this.visitedLinks.includes(currentLink)) {
        this.visitedLinks.push(currentLink);
        localStorage.setItem('visitedLinks', JSON.stringify(this.visitedLinks));
      }
    },
  trackVisitedLinks() {
  // Check if local storage is available
  if (localStorage) {
    const visitedLinks = JSON.parse(localStorage.getItem('visitedLinks')) || [];

    window.onpopstate = function(event) {
      const currentURL = document.location.href;

      // Check if URL exists in visitedLinks
      if (!visitedLinks.includes(currentURL)) {
        visitedLinks.push(currentURL);
        localStorage.setItem('visitedLinks', JSON.stringify(visitedLinks));
      }
    }
  }
},

// Check for local storage before calling the function
if (localStorage) {
  trackVisitedLinks();
},

    fetchData() {
      fetch(`https://www.googleapis.com/customsearch/v1?key=API_KEY&q=${this.inputValue}`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
      })
        .then((response) => response.json())
        .then((data) => {
          this.fetchedData = data.items.map((item) => ({
            link: item.link,
            title: item.title,
            pagemap: item.pagemap,
          }));
        })
        .catch((error) => console.error(error));
    },
  },
};
</script>
