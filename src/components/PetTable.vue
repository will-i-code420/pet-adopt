<template>
  <div class="petTable-container">
    <h1>{{ species }} Looking For A New Home</h1>
    <b-table striped hover :items="pets">
      <template slot="name" slot-scope="data">
        <!-- `data.value` is the value after formatted by the Formatter -->
        <router-link :to="`/pets/${species}/${data.index}`">{{ data.value }}</router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
export default {
  props: {
    species: String,
    pets: Array
  }
}
</script>
