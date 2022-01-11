<template>
  <div class="nav-search">
    <h1>{{ title }}</h1>
    <div class="search-submit">
      <!-- <input type="text" name="search" id="search-field" placeholder="Search an image..."> -->
      <!-- <p>{{ searchDate }}</p> -->
      <p>Select a date using the calendar and then press the search button. <br>
         Or generate a single picture or multiple pictures.
      </p>
      <input type="date" v-model="searchDate" :max="currDate" title="Select a date..."> 
      <input type="submit" @click="submitDate" value="🔍" title="Search...">
    </div>
    <div class="buttons">
      <button class="picture-btn" id="single-btn" title="Single random picture..." @click="singleRandom">🖼️</button>
      <button class="picture-btn" id="mutiple-btn" title="Multiple random pictures..." @click="multipleRandom">🖼️🖼️ <br> 🖼️🖼️</button>
    </div>
    <!-- <div class="buttons">
      <button class="layout-buttons" id="list">List</button>
      <button class="layout-buttons" id ="gallery">Gall</button>
    </div> -->
  </div>
</template>

<script>
export default {
  name: 'NavSearch',
  props: {
    title: String
  },
  data () {
    return {
      currDate : new Date().toISOString().split('T')[0],
      searchDate: "",
    }
  },
  methods: {
    submitDate() {
      console.log('Submitting date...');
      this.$emit('query', this.searchDate)
    },
    singleRandom() {
      console.log('Single random picture...')
      this.$emit('single', 1)
    },
    multipleRandom() {
      console.log('Multiple random pictures...')
      this.$emit('multiple', 4)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.nav-search {
  display:  flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.layout-buttons {
  width: 32px;
  aspect-ratio: 1;
  margin: .5rem;
}

input[type=date] {
  width: 150px;
}

input[type=submit] {
  /*width:  500px;*/
  font-size: 16px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0.2rem;
}

input[type=submit]:hover {
  /*border: 1px solid #444;*/
  /*border: outset;*/
  background-color: #eee;
}

input {
  margin: 0.5rem;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.picture-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 48px;
  height: 48px;
  aspect-ratio: 1;
  /*padding-bottom: 4px;*/
  /*background: transparent;*/
}

#single-btn {
  font-size: 32px;
  padding-bottom: 4px;
}

.picture-btn:hover {
  border-color: #444;
}
</style>
