<template>
  <div class="image">
    <h3>{{elem.title}}</h3>
    <hr>
    <img :src=elem.url alt="Some alternative text">
    <hr>
    <div class="content">
      <p>{{elem.explanation}}</p>
      <br>
      <hr>
      <br>
      <span><strong>{{elem.date}}</strong></span>
    </div>
    <div class="interactive">
      <button v-if="!liked" class="like-btn" title="Like" @click="clickedLike">🤍</button>
      <button v-if="liked" class="like-btn" title="Dislike" @click="clickedLike">❤️</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Image',
  props: {
    elem: Object,
  },
// todo : use localStorage to keep track of likes / entire entries (as an object)
data() {
  return {
    liked: false,
    // elem: this.elem,
  }
},
mounted() {
    // if we've seen this image before, set the liked to true or false (depending if we liked it or not)
    if (localStorage[this.elem.date]) {
      this.liked = localStorage[this.elem.date];
    }
    console.log(this.elem.date);
    // console.log()
  },
  methods: {
    clickedLike() {
      this.liked = !this.liked;
      localStorage[this.elem.date] = this.liked;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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

p {
  font-size: 14px;
  width:  500px;
  text-align: left;
  text-indent: 3rem;
  line-height: 1.3rem;
}

img {
  width: 500px;
}

span {
  text-decoration: underline;
}

.image {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  border: 2px solid #444;
  padding: 1rem;
  border-radius: 1rem;
  box-shadow: 3px 3px 5px black;
}

.interactive {
  display: flex;
  justify-content: flex-end;
}

.like-btn {
  background: transparent;
  border: none;
  font-size: 24px;
  margin-right: 0.5rem;
}

.like-btn:hover {
  /*font-size: 25px;*/
  cursor: pointer;

}
</style>
