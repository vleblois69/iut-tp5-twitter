<template>
    <div>
        <div>
          <strong>{{ tweet.auteur.prenom }} {{ tweet.auteur.nom }}</strong>
          <span class="handle">@{{ tweet.auteur.handle }} - {{ moment(tweet.date).fromNow() }}</span>
        </div>
        <div>
          {{ tweet.contenu }}
         </div>
         <div>
          <ul>
            <li class="button">
              <icon name="reply"/>
            </li>
            <li class="button">
              <a @click="retweet()" v-if="isRetweetable()">
                <icon name="retweet"/> {{tweet.retweeters.length}}
              </a>
              <icon name="retweet" v-else/> {{tweet.retweeters.length}}
            </li>
            <li class="button">
              <icon name="heart"/>
            </li>
            <li class="button">
              <icon name="envelope"/>
            </li>
          </ul>
         </div>
    </div>
</template>

<script>
import 'vue-awesome/icons'
import moment from 'moment'
import Icon from 'vue-awesome/components/Icon'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  created: function () {
    moment.locale('fr')
  },
  name: 'tweet',
  components: {Icon},
  props: ['tweet', 'currentUser'],
  methods: {
    moment: function (date) {
      return moment(date)
    },
    retweet: function () {
      this.$http.get('http://localhost:8080/retweet', {params: {utilisateur: this.currentUser, tweet: this.tweet.id}, responseType: 'text'}).then(
      response => {
        this.$emit('retweeted', this.tweet.id)
      },
      response => {
        // error callback
      })
    },
    isRetweetable: function () {
      var currentUserIsAutor = this.currentUser === this.tweet.auteur.handle
      if (currentUserIsAutor) {
        return false
      } else {
        var userHasAlreadyRetweet = (this.tweet.retweeters.find(utilisateur => utilisateur.handle === this.currentUser) === undefined)
        return (userHasAlreadyRetweet)
      }
    }
  }
}
</script>

<style scoped>
  li.button {
   display: inline-block;
  }

  a {
   color: #42b983;
  }

  span.handle {
   color: gray;
  }
</style>
