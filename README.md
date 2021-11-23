## 介绍

使用 vue3 做的一个给图片添加自定义水印并导出的小工具

新手canvas筆記：
```javascript
const addWatermark = () => {
  canvas = document.getElementById(canvasId);
  ctx = canvas.getContext("2d");   //取得畫布(2d)
  img = document.createElement("img");
  img.onload = render;   //圖片載入完成後執行render渲染
  img.src = imgUrl.value;
};

const render = () => {
  canvas.width = img.width;   //設置畫布大小
  canvas.height = img.height;
  ox = canvas.width / 2;
  oy = canvas.height / 2;
  ctx.drawImage(img, 0, 0, img.width, img.height);   //將圖片放到畫布上同時縮放，後面兩個參數為縮放大小(單位:像素，PS:原點在左上)
  ctx.save();   //保存坐原点平移之前的状态
  ctx.translate(ox, oy);   //用来移动 canvas 的原点到指定的位置
  ctx.rotate((30 * Math.PI) / 180);   //旋轉坐標軸
  ctx.translate(-ox, -oy);   //平移回原點
  ctx.fillStyle = waterColor.value;   //设置图形的填充颜色
  ctx.font = `bold ${waterFontSize.value}px`;   //設置文字樣式
  for (
    let a = -img.width / clearance.value;
    a < img.width / clearance.value;
    a++
  ) {
    for (
      let b = -img.height / clearance.value;
      b < (img.height / clearance.value) * 2;
      b++
    ) {
      ctx.fillText(
        waterText.value,
        a * clearance.value * 2,
        10 + b * clearance.value
      );   //fillText(text, x, y [, maxWidth]) 在指定的 (x,y) 位置填充指定的文本，绘制的最大宽度是可选的
    }
  }
  ctx.restore();   //回復上一次儲存的畫布狀態
};
```
`let getUrl = canvas.toDataURL();`  取得canvas的base64資料連結

PS：要取得canvas圖片要在render之後
