<template>
  <FileUploader @process-image="setProductImage" :label="'Upload Profile Picture'" :file-types="'jpg, png'" />

  <button type="button" @click="upload()">Upload File</button>
</template>

<script setup>
import FileUploader from './components/file-uploader/ComponentOne.vue'
import { ref } from 'vue'
import axios from 'axios'

const image = ref()
const api ='http://127.0.0.1:8000/api/upload-file'

function setProductImage(val) {
  image.value = val
}

async function upload() {
  const config = {
    headers: { 'content-type': 'multipart/form-data' }
  }
  const formData = new FormData()
  formData.append('image', image.value)

  await axios.post(api, formData, config).then((response) => {
     console.log(response)
  })
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
