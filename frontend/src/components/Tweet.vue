<template>
    <div>
        {{ tweet.auteur }} : {{ tweet.contenu }}
    </div>
</template>

<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>

