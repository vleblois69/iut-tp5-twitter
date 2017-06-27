<template>
  <div class="hello">
    <select @change="onChange($event.target.value)">
    <option disabled value="">Choisissez un utilisateur ...</option>
    <option v-for="utilisateur in utilisateurs" :value="utilisateur.handle">
     {{ utilisateur.prenom }} {{ utilisateur.nom }}
    </option>
    </select>
     <feed :tweets="tweets" :loading="loading" @retweeted="retweet"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Utilisateur from './Utilisateur'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Feed, Utilisateur},
  data () {
    return {
      tweets: [],
      loading: true
    }
  },
  methods: {
    retweet: function (id) {
      var tweet = this.tweets.find(tweet => tweet.id === id)
      tweet.retweeters.push({handle: 'snoopdog'})
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
