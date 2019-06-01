<template>
  <div class="home-container">
    <h1>Find Your New Best Friend Today!</h1>
    <br>
    <p>We currently have <strong>{{ animalsCount }}</strong> pets looking for a new home</p>
    <br>
    <p>There are <strong>{{ getAllCats.length }}</strong> cats</p>
    <br>
    <p>There are <strong>{{ getAllDogs.length }}</strong> dogs</p>

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
          :value="null"
          :options="['Cats', 'Dogs']"
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

      <b-form-group label="Gender:">
        <b-form-radio-group
          v-model="formData.gender"
          :options="options"
          buttons
          button-variant="outline-primary"
          name="gender"
          >
        </b-form-radio-group>
      </b-form-group>

      <b-form-group id="input-group-4" label="Pet's Age:" label-for="input-4">
        <b-form-input
          id="input-4"
          v-model="formData.age"
          type="number"
          required
          placeholder="Enter Age"
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-5" label="Pet's Weight:" label-for="input-5">
        <b-form-input
          id="input-5"
          v-model="formData.weight"
          type="number"
          required
          placeholder="Enter Weight(LBS)"
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
          placeholder="(City, State, Zip)"
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

      <b-button type="submit" variant="primary" :disabled="!formComplete">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <v-container grid-list-xl>
	     <image-uploader v-model="avatar">
	        <div slot="imageActivator">
	           <v-avatar size="150px" v-ripple v-if="!avatar" class="grey lighten-3 mb-3">
               <span>Add Pet Photo</span>
	            </v-avatar>
	             <v-avatar size="150px" v-ripple v-else class="mb-3">
                 <img :src="avatar.imageURL" alt="avatar">
	              </v-avatar>
	          </div>
	      </image-uploader>
	       <v-slide-x-transition>
	          <div v-if="avatar && saved == false">
	             <v-btn class="primary" @click="uploadImage" :loading="saving">Save Photo</v-btn>
	          </div>
	       </v-slide-x-transition>
	    </v-container>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
import ImageUploader from '@/components/ImageUploader.vue'

export default {
  name: 'home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: '',
        species: null,
        breed: '',
        gender: '',
        weight: '',
        color: '',
        notes: '',
        location: ''
      },
      options: [
        { text: 'Male', value: 'male' },
        { text: 'Female', value: 'female' },
        { text: 'Other (Use Special Notes)', value: 'other *see notes' }
      ],
        avatar: null,
	      saving: false,
	      saved: false
    }
  },
  components: {
    ImageUploader: ImageUploader
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats',
      'getAllDogs'
    ]),
    formComplete () {
      return this.formData
    }
  },
  watch: {
    avatar: {
      handler: function () {
        this.saved = false
      },
      deep: true
    }
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
        age: '',
        species: null,
        breed: '',
        gender: '',
        weight: '',
        color: '',
        notes: '',
        location: ''
      }
    },
    uploadImage () {
      this.saving = true
      setTimeout(() => this.savedAvatar(), 1000)
    },
    savedAvatar () {
      this.saving = false
      this.saved = true
    }
  }
}
</script>
