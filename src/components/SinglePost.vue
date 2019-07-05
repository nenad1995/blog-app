<template>
  <div>
    <div>
      <h2>{{ post.title }}</h2>
      <div>{{ post.text }}</div>
      <div>
        Posted at {{ post.createdAt }}
      </div>
    </div>
  </div>
</template>

<script>
import { posts } from '../services/post-service'

export default {
  
  data () {
    return {
      post: {}
    }
  },

  beforeRouteEnter(to, from, next) {
    posts.get(to.params.id)
      .then((response) => {
        next((vm) => {
          vm.post = response.data
        })
      })
  }
}
</script>