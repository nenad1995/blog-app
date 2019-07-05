<template>
  <div>
    <form @submit.prevent="onSubmit">
      <div>
        <div>
          <input type="text" required="required" v-model="post.title" />
        </div>
        <div>
          <input type="text" required="required" v-model="post.text" />
        </div>
        <div>
          <button  type="submit">
            Submit
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

  methods: {
    onSubmit () {
      posts.add(this.post)
        .then((response) => {
          this.$router.push({ name: 'posts' })
        })
    }
  }
}
</script>