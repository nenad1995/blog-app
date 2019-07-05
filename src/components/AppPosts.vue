<template>
  <div>
    <div v-for="post in posts" :key="post.id">
      <h2>{{ post.title }}</h2>
      <div>{{ post.text }}</div>
      <div>Posted at : {{ post.createdAt }}</div>
    </div>
  </div>
</template>

<script>
import { posts } from '../services/post-service'

export default {
  data () {
    return {
      posts: []
    }
  },

  beforeRouteEnter (to, from, next) {
    posts.getAll()
      .then((response) => {
        next((vm) => {
          vm.posts = response.data
        })
      })
  }
}
</script>