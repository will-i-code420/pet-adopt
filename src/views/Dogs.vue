<template>
  <div class="">
    <h1>Dogs Looking For A New Home</h1>
    <b-table striped hover :items="dogs"></b-table>
  </div>
</template>

<script>
import dogs from '@/data/dogs'

export default {
  data () {
    return {
      dogs
    }
  }
}
</script>

<style lang="css" scoped>
</style>
