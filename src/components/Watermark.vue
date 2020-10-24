<template>
  <ToolView @changeImgUrl="changeImgUrl" />
  <canvas id="canvas"></canvas>
</template>

<script>
import { ref, reactive, onMounted } from 'vue'
import ToolView from './ToolView.vue'

export default {
  name: 'Watermark',
  setup () {
    let imgUrl = ref('')
    let waterText = ref('此证件仅供办理XX使用，他用无效')
    let waterColor = ref('#999')
    let waterFontSize = ref('12')
    let clearance = ref('100')
    let canvas, ctx, img, ox, oy

    const addWatermark = () => {
      canvas = document.getElementById('canvas')
      ctx = canvas.getContext('2d')
      img = document.createElement('img')
      img.onload = render
      img.src = imgUrl.value
    }

    const render = () => {
      canvas.width = img.width
      canvas.height = img.height
      ox = canvas.width / 2
      oy = canvas.height / 2

      ctx.drawImage(img, 0, 0, img.width, img.height)
      ctx.save()
      ctx.translate(ox, oy)
      ctx.rotate(30 * Math.PI/180)
      ctx.translate(-ox, -oy)
      ctx.fillStyle = waterColor.value
      ctx.font = `bold ${waterFontSize.value}px`

      for (let a = -img.width / clearance.value; a < img.width / clearance.value; a++) {
        for (let b = -img.height / clearance.value; b < img.height / clearance.value * 2; b++) {
          ctx.fillText(waterText.value, a * clearance.value * 2, 10 + b * clearance.value)
        }
      }
      
      ctx.restore()
    }

    const changeImgUrl = (val) => {
      imgUrl.value = val
      addWatermark()
    }

    return {
      changeImgUrl
    }
  },
  components: {
    ToolView
  }
}
</script>
