<script lang="ts" setup>
interface Props {
  label: string
  id: string
}

const fileName = ref('')

const props = defineProps<Props>()
const emit = defineEmits(['upload'])

const handleChange = (e: any) => {
  if (e.target.files[0]) {
    fileName.value = e.target.files[0].name
    emit('upload', e, props.id)
  } else {
    fileName.value = ''
  }
}
</script>


<template>
  <div class="relative-wrapper">
    <p>{{ label }}</p>
    <input :id="id" :name="id" type="file" @change="handleChange" />
    <label :for="id" class="uploader">
      <span class="info" v-if="fileName">
        {{ fileName }}
      </span>
      <span class="info" v-else>Click here to upload data</span>
      <span class="btn" v-if="!fileName">Upload</span>
    </label>

    <button class="cancel" @click.native="fileName = ''" v-if="fileName">X</button>
  </div>
</template>

<style scoped>
input {
  display: none;
}

.uploader {
  background: white;
  color: black;
  padding: 20px 25px;
  display: flex;
  align-items: center;
  border-radius: 8px;
  cursor: pointer;
  min-height: 88px;
}

.uploader span.info {
  flex: 1;
  color: #999;
}

.uploader .btn {
  background: #f2f2f2;
  border: none;
  padding: 12px 20px;
  border-radius: 8px;
  cursor: pointer;
  color: #999;
}

.cancel {
  background: #f2f2f2;
  border: none;
  padding: 12px 20px;
  border-radius: 8px;
  cursor: pointer;
  color: #999;
  position: absolute;
  right: 20px;
  top: 42px;
}

.relative-wrapper {
  position: relative;
}
</style>
