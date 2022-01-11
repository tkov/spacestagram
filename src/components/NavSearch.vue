<template>
  <div class="nav-search">
    <h1>{{ title }}</h1>
    <div class="search-submit">
      <input type="text" name="search" id="search-field" placeholder="Search an image...">
      <input type="submit" value="Submit">
    </div>
    <div class="buttons">
      <button class="layout-buttons" id="list">List</button>
      <button class="layout-buttons" id ="gallery">Gall</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NavSearch',
  props: {
    title: String
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
</style>
