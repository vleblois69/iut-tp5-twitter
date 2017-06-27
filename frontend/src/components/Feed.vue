<template>
    <div>
        <ul>
              <li v-for="tweet in tweets">
                <tweet :tweet="tweet"/>
              </li>
         </ul>
    </div>
</template>

<script>
export default {
  name: 'feed',
  props: ['tweet']
}
</script>

