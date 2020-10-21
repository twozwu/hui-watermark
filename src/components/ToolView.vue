<template>
  <input type="file" id="imgFile" accept="image/png,image/jpeg,image/gif,image/jpg" @change="selectImg">
  <label for="imgFile">上传图片</label>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'ToolView',
  setup(props, {emit}) {

    const selectImg = (event) => {
      const file = event.target.files[0]
      const reader = new FileReader()
      reader.onload = () => emit('changeImgUrl', reader.result)
      reader.readAsDataURL(file)
    }

    return {
      selectImg
    }
  },
  emits: ['changeImgUrl']
}
</script>

<style lang="">
  #imgFile {
    display: none;
  }
</style>
