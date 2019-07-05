<template>
  <div>
    <div>
      <h2>{{ post.title }}</h2>
      <div>{{ post.text }}</div>
      <div>
        Posted at {{ post.createdAt }}
      </div>
    </div>
    <add-comment @commentAdded="addComment">Add Comment</add-comment>
    <comment-list :comments="comments"></comment-list>
  </div>
</template>

<script>
import { posts } from '../services/post-service'
import AddComment from './AddComment.vue'
import CommentList from './CommentList.vue'

export default {

  components: {
    AddComment,
    CommentList
  },

  data () {
    return {
      post: {}
    }
  },

  methods: {
    addComment (comment) {
      posts.addComment(comment, this.post.id)
        .then((response) => {
          posts.get(this.post.id)
            .then((response) => {
              this.post = response.data
            })
        })
    }
  },

  computed: {
    comments () {
      return this.post.comments
    }
  },

  beforeRouteEnter (to, from, next) {
    posts.get(to.params.id)
      .then((response) => {
        next((vm) => {
          vm.post = response.data
        })
      })
  }
}
</script>