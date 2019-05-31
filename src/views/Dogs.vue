<template>
  <div class="dog-container">
    <PetTable
    species="Dogs"
    :pets="dogs"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import PetTable from '@/components/PetTable.vue'

export default {
  name: 'dogs',
  components: {
    PetTable
  },
  data () {
    return {}
  },
  computed: {
    ...mapState([
      'dogs'
    ])
  }
}
</script>

<style lang="css" scoped>
</style>
