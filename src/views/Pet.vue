<template>
  <div class="">
    <h1>{{ animal.name }} ({{ $route.params.species }})</h1>
    <p>Age: {{ animal.age }} years old</p>
    <p>Weight: {{ animal.weight }} lbs</p>
    <p>Breed: {{ animal.breed }}</p>
    <p>Gender: {{ animal.gender }}</p>
    <p>Color: {{ animal.color }}</p>
    <p>About: {{ animal.notes }}</p>
    <p>Location: {{ animal.location }}</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      animal: {}
    }
  },
  computed: {
    ...mapState([
      'cats',
      'dogs'
    ])
  },
  created () {
    const species = this[this.$route.params.species][this.$route.params.id]
    this.animal = species
  }
}
</script>

<style lang="css" scoped>
</style>
