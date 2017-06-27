<template>
    <div>
        {{ tweet.auteur.handle }} : {{ tweet.contenu }}
    </div>
</template>

<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>

