<template>
  <div>
    <form @submit.prevent="onSubmit" @reset="reset">
      <div>
        <div>
          <input type="text" required="required" minlength="2" v-model="post.title" />
        </div>
        <div>
          <input type="text" required="required" maxlength="300" v-model="post.text" />
        </div>
        <div>
          <button  type="submit">
            {{ isEditing ? 'Edit' : 'Submit' }}
          </button> 
          <button type="reset">
            Reset
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { posts } from '../services/post-service'

export default {
  data () {
    return {
      post: {
        title: '',
        text: ''
      }
    }
  },

  created() {
    if (this.$route.params.id) {
      this.isEditing = true
      posts.get(this.$route.params.id)
        .then((response) => {
          this.post = response.data
        })
    }
  },

  methods: {
    onSubmit() {
      if (this.$route.params.id) {
        this.editPost()
      } else {
        this.addPost()
      }
    },

    addPost() {
      posts.add(this.post)
        .then((response) => {
          this.$router.push({ name: 'posts' })
        })
    },

    editPost() {
      posts.update(this.post)
        .then((response) => {
          this.$router.push({ name: 'posts' })
        })
    },

    reset() {
      this.post.title = ''
      this.post.text= ''
    }
  }
}
</script>