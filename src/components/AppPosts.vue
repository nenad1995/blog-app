<template>
  <div>
    <div v-for="(post, index) in posts" :key="post.id">
      <h2>{{ post.title }}</h2>
      <div>{{ post.text }}</div>
      <div>Posted at : {{ post.createdAt | formatDate }}</div>
      <div>
        <div>
          <router-link :to="{ name:'view', params: { id: post.id } }">
            View Post
          </router-link>
          <router-link :to="{ name:'edit', params: { id: post.id } }">
            Edit Post
          </router-link>
          <button @click="deletePost(post.id, index)">
            Delete Post
          </button>
        </div>
        <div>
          <h3>Number of comments: {{ post.comments.length }}</h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { posts } from '../services/post-service'
import { DateMixin } from '../mixins'

export default {
  data () {
    return {
      posts: []
    }
  },

  mixins: [ DateMixin ],

  methods: {
    deletePost(id, index) {
      posts.remove(id)
        .then((response) => {
          this.posts.splice(index, 1)
        })
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