<template>
  <div class="hello">
    <utilisateurs :utilisateurs="utilisateurs" @userSelected="changeUser"/><br>
    <postTweet @tweetCreated="createTweet"/>
    <feed :tweets="tweets" :loading="loading" :currentUser="currentUser" @retweeted="retweet"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Utilisateurs from './Utilisateurs'
import PostTweet from './PostTweet'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Feed, Utilisateurs, PostTweet},
  data () {
    return {
      tweets: [],
      utilisateurs: [],
      loading: true,
      currentUser: null,
      messageTweet: ''
    }
  },
  methods: {
    retweet: function (id) {
      var tweet = this.tweets.find(tweet => tweet.id === id)
      tweet.retweeters.push({handle: this.selectedUser})
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
    },
    changeUser: function (handle) {
      this.currentUser = handle
    },
    createTweet: function (message) {
      this.$http.get('http://localhost:8080/tweet', {params: {auteur: this.currentUser.handle, contenu: message}}).then(response => {
        var createdTweet = response.body
        createdTweet.date = Date.now()
        createdTweet.retweeters = []
        console.log(createdTweet)
        this.tweets.push(createdTweet)
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
