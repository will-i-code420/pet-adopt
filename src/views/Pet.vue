<template>
  <div class="">
    <h1>{{ animal.name }} ({{ $route.params.species }})</h1>
    <p>Age: {{ animal.age }} years old</p>
    <p>Weight: {{ animal.weight }} lbs</p>
    <p>Breed: {{ animal.breed }}</p>
    <p>{{ animal.gender }}</p>
    <p>Color: {{ animal.color }}</p>
    <p>About: {{ animal.notes }}</p>
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
  mounted () {
    const animal = this[this.$route.params.species][this.$route.params.id]
    this.animal = animal
  }
}
</script>

<style lang="css" scoped>
</style>
