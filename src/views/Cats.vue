<template>
  <div class="">
    <h1>Cats Looking For A New Home</h1>
    <b-table striped hover :items="cats">
      <template slot="name" slot-scope="data">
        <!-- `data.value` is the value after formatted by the Formatter -->
        <router-link :to="`/pets/$(data.index)`">{{ data.value }}</router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      cats
    }
  }
}
</script>

<style lang="css" scoped>
</style>
