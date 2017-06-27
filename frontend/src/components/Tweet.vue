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
              <icon name="retweet"/>
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

export default {
  created: function () {
    moment.locale('fr')
  },
  name: 'tweet',
  components: {Icon},
  props: ['tweet'],
  methods: {
    moment: function (date) {
      return moment(date)
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
