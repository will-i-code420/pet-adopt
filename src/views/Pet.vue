<template>
  <div class="pet-container">
    <h1>{{ animal.name }} ({{ $route.params.species }})</h1>
    <p>Age: {{ animal.age }} years old</p>
    <p>Weight: {{ animal.weight }} lbs</p>
    <p>Breed: {{ animal.breed }}</p>
    <p>Gender: {{ animal.gender }}</p>
    <p>Color: {{ animal.color }}</p>
    <p>About: {{ animal.notes }}</p>
    <p>Location: {{ animal.location }}</p>
    <br>
    <br>
    <p>If you're interested in brining {{ animal.name }} home fill out the form below and we'll be in touch within 24 hours</p>
    <button @click="toggleAdoptInfo" class="btn btn-primary">I'm Interested</button>
    <b-form @submit.prevent="submitAdoptInfo" v-if="showAdoptForm">
      <b-form-group id="input-group-10" label="Name:" label-for="input-10">
        <b-form-input
          id="input-10"
          v-model="adoptInfo.name"
          required
          placeholder="Enter Full Name"
        >
        </b-form-input>
      </b-form-group>
      <b-form-group id="input-group-11" label="Phone #:" label-for="input-11">
        <b-form-input
          id="input-11"
          v-model="adoptInfo.phone"
          type="tel"
          required
          placeholder="Good Contact #"
        >
        </b-form-input>
      </b-form-group>
      <b-form-group id="input-group-12" label="Email:" label-for="input-12">
        <b-form-input
          id="input-12"
          v-model="adoptInfo.email"
          type="email"
          required
          placeholder="Good Email"
        >
        </b-form-input>
      </b-form-group>
      <b-form-group label="Preferred Contact Method">
        <b-form-radio-group
          v-model="adoptInfo.contactMethod"
          :options="options"
          buttons
          button-variant="outline-primary"
          name="contactMethod"
          >
        </b-form-radio-group>
      </b-form-group>
      <b-form-group id="input-group-13" label="Current # of Pets:" label-for="input-13">
        <b-form-input
          id="input-13"
          v-model="adoptInfo.petsOwned"
          type="number"
          required
          placeholder="How many other pets do you have?"
        >
        </b-form-input>
      </b-form-group>
      <b-form-group id="input-group-14" label="A little about you:" label-for="input-14">
        <b-form-input
          id="input-14"
          v-model="adoptInfo.ownerInfo"
          required
          placeholder="Tell us about you and why you're interested in adopting"
        >
        </b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary" :disabled="!formComplete">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'pet',
  data () {
    return {
      showAdoptForm: false,
      adoptInfo: {
        name: '',
        phone: '',
        email: '',
        contactMethod: '',
        petsOwned: '',
        ownerInfo: ''
      },
      options: [
        { text: 'Phone', value: 'phone call' },
        { text: 'SMS', value: 'text message' },
        { text: 'Email', value: 'email' }
      ],
      animal: {}
    }
  },
  computed: {
    ...mapState([
      'cats',
      'dogs'
    ]),
    formComplete () {
      return this.adoptInfo
    }
  },
  methods: {
    toggleAdoptInfo () {
      this.showAdoptForm = !this.showAdoptForm
    },
    submitAdoptInfo () {}
  },
  created () {
    const species = this[this.$route.params.species][this.$route.params.id]
    this.animal = species
  }
}
</script>

<style lang="css" scoped>
</style>
