<template>
  <div class="hello">
     <feed :tweets="tweets"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Feed},
  data () {
    return {
      tweets: [{auteur: 'bob'}]
    }
  },
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
      },
      response => {
        // error callback
      })
    }
  },

  created: function () {
    this.fetchTweets()
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
