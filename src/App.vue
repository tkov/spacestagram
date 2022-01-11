<template>
  <header>
  <NavSearch title="Spacestagram" @query="getQueryAndFetch" @single="fetchSingle" @multiple="fetchMultiple"/>
  </header>
  <main>
    <section class="images">
    <div>
      <!-- We are done loading and have data to process... -->
      <ul v-if="!loading && retData && retData.length">
        <Image v-for="elem of retData" v-bind:key="elem.date" :elem="elem">
        </Image>
      </ul>
     <!--  {{ retData }} -->
    </div>
    <p v-if="loading">
     Still loading..
    </p>
    <p v-if="errorMsg">

    </p>
    </section>
  </main>
  <footer></footer>
</template>

<script>
import NavSearch from './components/NavSearch.vue'
import Image from './components/Image.vue'

// const data = ref(null);
// const loading = ref(true);
// const error = ref(null);

export default {
  name: 'App',
  components: {
    NavSearch,
    Image,
  },
  data() {
    return {
      loading: null,
      errorMsg: null,
      retData: null,
      query: '',
    }
  },
  methods: {
    getQueryAndFetch(query) {
      console.log('The query is ', query)
      const date = '&date=' + query
      this.fetchData(date);
    },
    fetchSingle(count){
      const query = '&count=' + count;
      this.fetchData(query)
    },
    fetchMultiple(count){
      const query = '&count=' + count;
      this.fetchData(query)
    },
    fetchData(query) {

      this.loading = true;
      fetch('https://api.nasa.gov/planetary/apod?api_key=J17V0hW5w8sLMz5FG024ZA54QbdDUdh9fQPMKgLz' + query, {
        method: 'get',
        headers: {
          'content-type': 'application/json'
        }
       })
      .then(async res => {
      const data = await res.json();

      // check for error response
      if (!res.ok) {
        // get error message from body or default to response statusText
        const err = (data && data.message) || res.statusText;
        return Promise.reject(err);
      }

      // console.log(data.length);

      if (data.length == undefined) {
        this.retData = Array(data);
      }
      else{
        this.retData = data;
      }
    })
    .catch(err => {
      this.errorMsg = err;
      console.error("There was an error!", err);
    });

    this.loading = false;

    } // fetchData()

  }, // methods
    // on initial load 4 random images
  mounted() {
    this.fetchData('&count=4');
  },
  update() {
    if (this.query == ''){
      console.log('New query...')
    }
  }
}

</script>

<style>
*, *::before, *::after {
  margin:  0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.images, ul {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

ul {
  list-style: none;
}
</style>
