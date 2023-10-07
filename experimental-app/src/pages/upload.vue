<script lang="ts" setup>
interface uploadType {
  type: string
  file: any
}
const allUploads = ref<uploadType[]>([])

const handleUpload = (e: any, type: string) => {
  allUploads.value.push({
    type,
    file: e.target.files[0]
  })
}

const handleUploadSubmit = () => {
  console.log(allUploads.value)
}
</script>

<template>
  <div>
    <MyUploader label="First Upload" id="first_upload" @upload="handleUpload" />
    <br />
    <br />
    <MyUploader label="Second Upload" id="second_upload" @upload="handleUpload" />
    <br />
    <br />
    <MyUploader label="Third Upload" id="third_upload" @upload="handleUpload" />

    <div>
      <pre>
        {{ allUploads }}
      </pre>
    </div>

    <div>
      <button @click="handleUploadSubmit()">Upload</button>
    </div>
  </div>
</template>
