## loading图绘制
话不多说，直接上手代码
### html 部分
`html` 部分比较简单，上完代码就直接跳过了
```HTML
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>canvas-loading</title>
    <script type="text/javascript" src="./index.js"></script>
  </head>
  <body>
    <canvas id="canvas">您的浏览器不支持canvas</canvas>
  </body>
</html>
```

### js代码分析
我们上代码先
*我们先把画布定成 600 x 400 的比例*
```js
const canvas = document.getElementById("canvas");
const CanWidth = canvas.width = 600;     // 画布宽
const CanHeight = canvas.height = 400;   // 画布高
```
2.定圆心的位置
```js
...
const [ rX, rY ] = [ CanWidth / 2, CanHeight / 2 ];
```
3.定圆的半径
```js
const R = 60;
```
4.定起始位置和结束位置
*这里有必要说一下，整个圆环旋转是通过结束角eAngle的变化来产生圆环在转的视觉的*
```js
...
let range = 0; // 我们定义一个 range 取值在0-100
const sAngle = 0;   // 定义起始角
const eAngle = (2 * Math.PI) / 100;     // 定义结束角
// 这里的eAngle的除于100是为了将一个圆分成100分，配合range
```
5.定义绘制函数
```js
function DrawRadius () {
  // 执行前判断当前range的值
  if (range < 100) {
    // 若range小于100,则range自加1，如果加快速度可以改变自加的值
    range++;
    // 清楚可视区域的画布
    ctx.clearRect(0, 0, CanWidth, CanHeight);
  } else {
    // 若是range大于或者等于100,则停止往下执行
    range = 0;
    return;
  }
  ctx.beginPath();
  ctx.lineWidth = 3;    // 圆环线条的粗细调整
  ctx.strokeStyle = '#1c86d1';  // 圆环线条的颜色调整
  /**
   * 绘制圆的函数
   * ctx.arc(x, y, r, sAngle, eAngle)
   * @param {number} x [圆心x坐标]
   * @param {number} y [圆心y坐标]
   * @param {number} r [圆半径]
   * @param {number} sAngle [起始角]
   * @param {number} eAngle [结束角]
   */
  ctx.arc(rX, rY, R, sAngle, eAngle * range);
  ctx.stroke();
  // 定时器调用
  requestAnimationFrame(DrawRadius);
};
```
6.执行函数呗
```js
DrawRadius();
```
简单的loading就已经Ok了
