## Canvas

Canvas API提供了通过JavaScript和HTML的\<canvas>元素来绘制图形的方法。它可以用于动画、游戏画面、数据可视化、图片编辑、实时视频处理等。

\<canvas>标签只有width和height两个属性，并且是可选的。默认宽高为300px*150px。当画布大小和其CSS设置的大小不一致时，canvas图像会伸缩以适应canvas元素容器的大小，这会导致扭曲。

获取**渲染上下文**：`canvas.getContext('2d')`。canvas的绘画功能都是通过它的渲染上下文来实现的。

**坐标系统**：左上角为原点(0, 0)，向右为x正方向，向下为y轴正方向。

**线宽**： 线宽是指给定路径的中心到两边的粗细。换句话说就是在路径的两边各绘制线宽的一半。因为画布的坐标并不和像素直接对应，当需要获得精确的水平或垂直线的时候要特别注意。 宽度是 1.0 的线条，实际填充区域仅仅延伸至路径两旁各一半像素。而这半个像素又会以近似的方式进行渲染，这意味着那些像素只是部分着色，结果就是以实际笔触颜色一半色调的颜色来填充整个区域。这就是为何宽度为 1.0 的线并不准确的原因。*解决方案：*1. 线条使用类似1.5这样的定位，以使线条边缘正好落在像素边界；2. 使用偶数线宽，可以将canvas画布设为2倍，再结合设置CSS样式使其缩小回来（待验证）。

**填充规则**： 当我们用到 `fill`（或者 [`clip`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/clip)和[`isPointinPath`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/isPointInPath) ）你可以选择一个填充规则，该填充规则根据某处在路径的外面或者里面来决定该处是否被填充，这对于自己与自己路径相交或者路径被嵌套的时候是有用的。可选值：`nonzero`（非零环绕规则，默认）、`evenodd`（奇偶环绕规则） 。

### 绘制命令

1. `ctx.canvas`，获取当前上下文所属的canvas元素

2. 绘制和清空矩形

   - `fillRect(x, y, width, height)`
   - `strokeRect(x, y, width, height)`
   - `clearRect(x, y, width, height)`

3. 命令

   - `beginPath()`
   - `closePath()`
   - `stroke()`
   - `fill()`
   - `save()` 保存画布的所有状态，canvas状态存储在栈中，绘画状态包括样式、变换和当前的裁切路径（clipping path）
   - `restore()` 恢复canvas画布的状态，从栈中弹出上一个保存的状态

4. 路径命令

   - `moveTo(x, y)`
   - `lineTo(x, y)`
   - `arc(x, y, radius, startAngle, endAngle, anticlockwise = false)` (x, y)是圆心位置，使用弧度，默认顺时针
   - `arcTo(x1, y1, x2, y2, radius)`  (x1, y1)和(x2, y2)是两个控制点，绘制的线不一定经过这两个点。根据这两个控制点和半径画弧，再将弧线起点和这个命令前的点用直线连起来。
   - `quadraticCurveTo(xp1x, cp1y, x, y)` 二次贝塞尔曲线
   - `bezierCurveTo(xp1x, cp1y, cp2x, cp2y, x, y)` 三次贝塞尔曲线
   - `rect(x, y, width, height)` 矩形路径，但不会绘制出来
   - `ellipse(cx, cy, rx, ry, rotation, startAngle, endAngle, anticlockwise = false)`，椭圆路径，实验阶段，使用弧度

5. Path2D对象

   - 通过Path2D对象可以用来缓存或记录绘画命令，简化代码和提高性能

   - `new Path2D()` 创建空的Path对象
   - `new Path2D(path)` 克隆Path对象
   - `new Path2D(d)` 从SVG建立Path对象
   - `path.addPath(path2[, transform])` 添加一条路径到当前路径，transform是一个可选的变换矩阵对象
   - 将Path2D对象实例作为参数传递给`stroke(path)`和`fill(path)`方法，来实现绘制该Path2D路径而不是当前路径

6. 样式

   - `fillStyle = color` color可以使颜色字符串、渐变对象或图案对象，默认为黑色#000
   - `strokeStyle = color`
   - `globalAlpha = transparencyValue` 全局透明度，0.0~1.0，在需要绘制大量拥有相同透明度的图形时相当高效。
   - `lineWidth = value` 线条宽度
   - `lineCap = type` 线条末端样式，默认butt、round、square
   - `lineJoin = type` 线条与线条接合处的样式
   - `miterLimit = value` 限制当两条线相交时交接处最大长度； 所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。 
   - `getLineDash()` 返回一个包含当前虚线样式，长度为非负偶数的数组
   - `setLineDash(segments)` 设置当前虚线样式，参数是个偶数个数的数组
   - `lineDashOffset = value` 设置虚线样式的其实偏移量

7. 渐变

   - `createLinearGradient(x1, y1, x2, y2)` 线性渐变
   - `createRadialGradient(cx1, cy1, r1, cx2, cy2, r2)` 径向渐变，(cx1, cy1, r1) 和 (cx2, cy2, r2)分别定义两个圆
   - `gradient.addColorStop(position, color)` position为0.0~1.0的数值，表示颜色所在的相对位置，color是CSS颜色值

8. 图案样式 Patterns

   - `createPattern(image, type)`image可以使一个Image对象的引用，或者另一个canvas对象。type必须是以下字符串值之一：repeat | repeat-x | repeat-y | no-repeat。

9. 阴影 Shadows

   - `shadowOffsetX = float` 引用在X轴的延伸距离，不受变换矩阵影响。默认为0，可以是负值
   - `shadowOffsetY = float` 基本同上
   - `shadowBlur = float` 设定阴影的模糊程度，其数值并不跟像素数量挂钩，也不受变换矩阵影响，默认为0
   - `shadowColor = color` 阴影颜色，标准的CSS颜色值，默认为全透明的黑色

10. 绘制文本

    - `fillText(text, x, y[, maxWidth])`
    - `strokeText(text, x, y[, maxWidth])`
    - `font = value`， 默认为`10px sans-serif`，和CSS `font`属性相同的语法，必须包含font-size和font-family
    - `textAlign = value`，文本对齐方式，可选值：start（默认） | end | left | right | center
    - `textBaseline = value`，基线对齐方式，可选值：top | hanging | middle | alphabetic（默认）| ideographic | bottom
    - `direction = value`，文本方向，可选值：ltr | rtl | inherit（默认）
    - `measureText(text)`，返回一个`TextMetrics`对象，包含宽度、所在像素

11. 绘制图片

    - 支持浏览器支持的任意格式图片，也可以使用页面中其他canvas元素作为图片源，支持以下类型：
      - `HTMLImageElement`：由Image()函数构造出来，或者任何\<img>元素
      - `HTMLVideoElement`：用一个\<video>元素作为图片源，可以从视频中抓取当前帧作为一个图像
      - `HTMLCanvasElement`：可以使用另一个\<canvas>元素作为图片源
      - `ImageBitmap`：这是一个高性能位图，可以低延迟地绘制，可以从上述所有源以及其他几种源中生成
    - `drawImage(image, x, y)`，(x, y)是在canvas中的起始坐标
    - `drawImage(image, x, y, width, height)`，width和height用来控制绘制图片时应该缩放的大小
    - `drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)`，裁取源图片中(sx, sy, sWidth, sHeight)位置和大小的部分，绘制到canvas的(dx, dy, dWidth, dHeight)位置和大小区域内

12. 矩阵变换

    - `translate(x, y)`，平移，会改变canvas的原点位置

    - `rotate(angle)`，旋转，弧度单位，旋转的中心店是canvas原点，要改变原点需要用translate方法

    - `scale(x, y)`，缩放，参数为负数时，相当于以x或y轴作为对称轴镜像反转

    - `transform(m11, m12, m21, m22, dx, dy)`，将当前的变换矩阵乘上一个基于自身参数的矩阵

      ```
      m11 m21 dx
      m12 m22 dy
      0   0   1
      ```

      m11：水平方向的缩放

      m12：水平方向的倾斜偏移

      m21：竖直方向的倾斜偏移

      m22：竖直方向的缩放

      dx： 水平方向的移动

      dy：竖直方向的移动

    - `setTransform(m11, m12, m21, m22, dx, dy)`，这个方法会将当前的变形矩阵重置为单位矩阵，然后用相同的参数调用 `transform `方法 

    - `resetTransform()`，重置当前变形为单位矩阵，相当于：`ctx.setTransform(1, 0, 0, 1, 0, 0)`

13. 组合

    - `globalCompositeOperation = type`，设置要在绘制新形状时应用的合成操作的类型，可选值有：source-over（默认）| source-in | source-out | source-atop | destination-over 等等

14. 裁切路径

    - `clip()`，将当前正在构建的路径转换为当前的裁切路径，裁切路径用于遮罩，隐藏不需要的部分，裁切需要的图形，本身不会绘制。默认情况下，canvas有一个和它一样大的裁切路径（也就是没有裁切效果）。一般最好结合save()/restore()使用

15. 事件交互的关键判断方法

    - `isPointInPath()`，判断当前路径是否包含检测点，返回结果是boolean值。path参数是Path2D路径。

      ```js
      isPointInPath(x, y[, fillRule])
      isPointInPath(path, x, y[, fillRule])
      ```

    - `isPointInStroke()`，判断点是否在路径的描边线上。

      ```js
      isPathInStroke(x, y)
      isPathInStroke(path, x, y)
      ```

### 动画

1. 通常的步骤
   1. 清空canvas
   2. 保存canvas状态
   3. 绘制动画图形
   4. 恢复canvas状态
2. `requestAnimationFrame(callback)`，告诉浏览器希望执行一个动画，并在重绘之前，请求浏览器执行一个特定的函数来更新动画
3. 长尾效果： 若用一个半透明的fillRect()函数取代clearRect()，就可轻松制作长尾效果。 

### ImageData对象

1. 只读属性
   - `width`，图片宽度，单位是像素
   - `height`，图片高度，单位是像素
   - `data`，`Unit8ClampedArray`类型的一维数组，包含着RGBA格式的整型数据，范围在0~255之间（包括255）。
2. 创建ImageData对象
   - `createImageData(width, height)`，创建一个新的、空白的ImageDat对象，所有像素被预设为透明黑
   - `createImageData(anotherImageData)`，创建一个和anotherImageData相同像素的ImageData对象，但是像素全被预设为透明黑，所以不是复制图片数据
3. 获取场景像素数据
   - `getImageData(left, top, width, height)`，获取参数表示的画布区域的像素数据，在画布意外的元素会被返回成一个透明黑的ImageData对象
4. 写入像素数据
   - `putImageData(imageData, dx, dy)`，(dx, dy) 是用来绘imageData对象左上角像素的绘图环境中的坐标
5. 反锯齿
   - `imageSmoothingEabled = true`，默认开启，不同浏览器需要不痛前缀

### 保存图片

1. `canvas.toDataURL('image/png')`，默认设定，创建一个PNG图片（的url）,返回的图片分辨率是96dpi
2. `canvas.toDataURL('image/jpeg', quality)`，创建一个JPG图片，quality范围0~1,1表示最好品质，0基本不被辨析，但文件小
3. `canvas.toBlob(callback, type, encoderOptions)`，创建一个在画布中的代表图片的Blob对象，[MDN]( https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement/toBlob )

生成的图片数据链接，可以直接用于\<image>或\<img>元素；如果用于一个有`download`属性的超链接`a`元素，则可以通过事件来保存到本地。

### 性能优化

1. 在离屏canvas上预渲染相似的图形或重复的对象

   **离屏canvas**：可以认为就是指页面上不可见的canvas。1. 可以通过createElement创建，但不添加到DOM中；2. 渲染但通过CSS处理成不可见应该也可行；3. 通过实验性API`OffscreenCanvas()`构造函数创建

2. 避免浮点数的坐标点，用整数取而代之

   当你画一个没有整数坐标点的对象时会发生子像素渲染。 浏览器为了达到抗锯齿的效果会做额外的运算。所以调用drawImage()时，用Math.floor()对所有坐标点取整是最好的。

3. 不要在用drawImage时缩放图像

   在离屏canvas中缓存图片的不痛尺寸

4. 使用错层画布去画一个复杂的场景

5. 用CSS设置大的背景图

   可以的话，背景图不通过canvas来绘制

6. 用CSS transforms特性缩放画布

   CSS transforms特性由于调用GPU，因此更快捷。最好的情况是，不要将小画布放大，而是去将大画布缩小。

7. 关闭透明度

   如果绘制时不需要透明，可以关闭透明度：`canvas.getContext('2d', { alpha: false })`

8. 其他

   - 尽可能避免shadowBlur属性
   - 使用不同的办法去清除画布（clearRect() vs. fillRect() vs. 调整canvas大小）
   - 动画使用requestAnimationFrame而非setInterval()
   - 等等

### 参考资源

1. [canvas ——MDN]( https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial )