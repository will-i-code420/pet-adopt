<template>
  <div class="imageUploader">
    <div @click="launchFilePicker()">
      <slot name="imageActivator"></slot>
      <input type="file" ref="file"
      :name="uploadField"
      @change="onFileChange($event.target.name, $event.target.files)"
      style="display:none"
      >
      <v-dialog v-model="errorDialog" max-width="300">
        <v-card>
          <v-card-text class="subheading">
            {{errorText}}
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn @click="errorDialog = false" flat>
              Got It!
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="css" scoped>
</style>
