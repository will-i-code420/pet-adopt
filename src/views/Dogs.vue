<template>
  <div class="">
    <h1>Dogs Looking For A New Home</h1>
    <b-table striped hover :items="dogs">
      <template slot="name" slot-scope="data">
        <!-- `data.value` is the value after formatted by the Formatter -->
        <router-link :to="`/pets/$(data.value)`">{{ data.value }}</router-link>
      </template>
    </b-table>
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
