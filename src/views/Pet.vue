<template>
  <div class="">
    {{ $route.params.species}}
    {{ $route.params. }}
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {}
  },
  computed: {
    ...mapState([
      'cats',
      'dogs'
    ])
  }
}
</script>

<style lang="css" scoped>
</style>
