<template>
  <div class="hello">
    <utilisateurs :utilisateurs="utilisateurs"/>
    <feed :tweets="tweets" :loading="loading" @retweeted="retweet"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Utilisateurs from './Utilisateurs'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Feed, Utilisateurs},
  data () {
    return {
      tweets: [],
      utilisateurs: [],
      loading: true
    }
  },
  methods: {
    retweet: function (id) {
      var tweet = this.tweets.find(tweet => tweet.id === id)
      tweet.retweeters.push({handle: 'ladygaga'})
    },
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
        this.loading = false
      },
      response => {
        // error callback
      })
    },
    fetchUtilisateurs: function () {
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
        this.utilisateurs = response.body
      },
      response => {
        // error callback
      })
    }
  },

  created: function () {
    this.fetchTweets()
    this.fetchUtilisateurs()
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
