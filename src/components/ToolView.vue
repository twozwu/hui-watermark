<template>
  <section>
    <input type="file" id="imgFile" accept="image/png,image/jpeg,image/gif,image/jpg" @change="selectImg">
    <label class="btn" for="imgFile">上传图片</label>

    <span class="btn" @click="download">下载图片</span>
  </section>
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

    const download = () => emit('downloadImg')

    return {
      selectImg,
      download
    }
  },
  emits: ['changeImgUrl', 'downloadImg']
}
</script>

<style lang="">
  #imgFile {
    display: none;
  }
  section {
    margin: 20px auto;
  }
  .btn {
    margin: 10px;
    padding: 3px 10px;
    border: 1px solid #DCDFE6;
    border-radius: 6px;
    color: #303133;
    cursor: pointer;
  }
</style>
