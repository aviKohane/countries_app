<template>
  <h1>List of countries</h1>
  <div v-if="isLoaded">
    <input type="text" placeholder="Search" class="search-input" v-model="searchValue">
    <CountriesGrid :searchValue="searchValue" :countries="countries" />
  </div>
  <div v-else class="loader">
  </div>
</template>

<script>
import CountriesGrid from './components/CountriesGrid.vue';

export default {
  name: 'App',
  components: {
    CountriesGrid
  },

  data() {
    return {
      searchValue: '',
      isLoaded: false,
      countries: [],

    }
  },
  created() {
    this.fetchData();
  },

  methods: {
    async fetchData() {
      const url = "https://restcountries.com/v3.1/all";
      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error(`Response status:${response.status}`);
        }
        this.countries = await response.json();
      } catch (error) {
        console.log(error.message);
        this.countries = [];
      }
      finally {
        this.isLoaded = true;

      }
    }
  }
}

</script>

<style>
#app {
  height: calc(100vh);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  align-items: center;
  align-items: center;
  flex-direction: column;
  background-color: white;
}

h1 {
  margin: 20px;
  color: #006cff;
}

.search-input {
  width: 200px;
  height: 30px;
  border-radius: 2px;
  margin-bottom: 5px;
}

/* HTML: <div class="loader"></div> */
.loader {
  width: 50vh;
  aspect-ratio: 1;
  background: #006cff;
  border-radius: 50%;
  animation: l1 3s infinite linear;
}

@keyframes l1 {
  12.5% {
    border-radius: 37% 63% 70% 30% / 30% 62% 38% 70%
  }

  25% {
    border-radius: 50% 50% 70% 30% / 52% 62% 38% 48%
  }

  37.5% {
    border-radius: 33% 67% 18% 82% / 52% 75% 25% 48%
  }

  50% {
    border-radius: 73% 27% 18% 82% / 52% 32% 68% 48%
  }

  62.5% {
    border-radius: 73% 27% 74% 26% / 64% 32% 68% 36%
  }

  75% {
    border-radius: 84% 16% 15% 85% / 55% 79% 21% 45%
  }

  87.5% {
    border-radius: 12% 88% 69% 31% / 10% 66% 34% 90%
  }
}
</style>
