<template>
    <div>
      <select @change="onChange($event.target.value)">
        <option disabled value="">Choisissez un utilisateur ...</option>
        <option v-for="utilisateur in utilisateurs" :value="utilisateur.handle">
          {{ utilisateur.prenom }} {{ utilisateur.nom }}
        </option>
      </select>
    </div>
</template>

<script>

export default {
  name: 'utilisateurs',
  props: ['utilisateurs'],
  methods: {
    onChange: function (handle) {
      var utilisateur = this.utilisateurs.find(utilisateur => utilisateur.handle === handle)
      this.$emit('userSelected', utilisateur)
    }
  }
}
</script>
