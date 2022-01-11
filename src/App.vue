<template>
  <header>
  <NavSearch title="Spacestagram"/>
  </header>
  <main>
    <section class="images">
    <Image></Image>
    </section>
  </main>
  <footer></footer>
</template>

<script>
import NavSearch from './components/NavSearch.vue'
import Image from './components/Image.vue'

export default {
  name: 'App',
  components: {
    NavSearch,
    Image,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.images {
  display: flex;
  flex-direction: column;
}
</style>
