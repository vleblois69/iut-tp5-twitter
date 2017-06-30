<template>
    <div>
      <textarea rows="4" cols="50" v-model="message"/>
      <br>
      <input type="submit" name="Tweet" @click="onClick()">
    </div>
</template>

<script>

export default {
  name: 'posttweet',
  data: {
    message: ''
  },
  methods:
  {
    onClick: function () {
      this.$emit('tweetCreated', this.message)
    }
  }
}
</script>
