<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
     <ul v-if="posts && posts.length">
       <li>Length: {{posts.length}}</li>
       <li v-for="post of posts" :key="post.id">
        <p><strong>{{post.title}}</strong></p>
        <p>{{post.body}}</p>
      </li>
      </ul>

      <ul v-if="errors && errors.length">
      <li v-for="error of errors" :key="error.id">
        {{error.message}}
      </li>
    </ul>
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
   
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: 'ObtainPosts',
  props: {
    msg: String,
  },

  data() {
    return {
      posts: [],
      errors: []
    }
  },
   // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
      this.posts = response.data
    } catch (e) {
      this.errors.push(e)
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
</style>
