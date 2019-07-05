<template>
  <form @submit.prevent="onSubmit">
    <hr />
    <h3>Add comment</h3>
    <div>
      <div>
        <input required="required" v-model="comment.text" />
      </div>
    </div>
    <div>
      <div>
        <button type="submit">
          Submit
        </button>
        <hr />
      </div>
    </div>
  </form>
</template>

<script>
export default {
  data () {
    return {
      comment: {
        text: ''
      }
    }
  },
  
  methods: {
    onSubmit () {
      this.$emit('commentAdded', this.comment)
    }
  }
}
</script>