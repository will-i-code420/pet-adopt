<template>
  <div class="home-container">
    <h1>Find Your New Best Friend Today!</h1>

    {{ getAllCats.length }}

    {{ getAllDogs.length }}

    {{ animalsCount }}

    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>
    <b-form @submit.prevent="submitPet" v-if="showPetForm">
      <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="formData.name"
          required
          placeholder="Enter name"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Species:" label-for="input-2">
        <b-form-select
          id="input-2"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        >
        </b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Breed:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="formData.breed"
          required
          placeholder="Enter Breed Type"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-9" label="Gender:" label-for="input-9">
        <b-form-input
          id="input-9"
          v-model="formData.gender"
          required
          placeholder="Enter Gender"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-4" label="Pet's Age:" label-for="input-4">
        <b-form-input
          id="input-4"
          v-model="formData.age"
          required
          placeholder="Enter Age"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-5" label="Pet's Weight:" label-for="input-5">
        <b-form-input
          id="input-5"
          v-model="formData.weight"
          required
          placeholder="Enter Weight in LBS"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-6" label="Pet's Color:" label-for="input-6">
        <b-form-input
          id="input-6"
          v-model="formData.color"
          required
          placeholder="Enter Color Description"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-7" label="Pet's Location:" label-for="input-7">
        <b-form-input
          id="input-7"
          v-model="formData.location"
          required
          placeholder="Current Pet Location"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-8" label="About Pet:" label-for="input-8">
        <b-form-input
          id="input-8"
          v-model="formData.notes"
          required
          placeholder="Any Special Info"
        >
        </b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null,
        breed: '',
        gender: '',
        weight: 0,
        color: '',
        notes: '',
        location: ''
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats',
      'getAllDogs'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    submitPet () {
      const { species, age, name, breed, gender, weight, color, notes, location } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age,
          species,
          breed,
          gender,
          weight,
          color,
          notes,
          location
        }
      }
      this.addPet(payload)
      this.formData = {
        name: '',
        age: 0,
        species: null,
        breed: '',
        gender: '',
        weight: 0,
        color: '',
        notes: '',
        location: ''
      }
    }
  },
  watchers: {

  }
}
</script>
