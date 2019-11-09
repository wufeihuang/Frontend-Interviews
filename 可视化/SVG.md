## SVG

SVG（Scalable Vector Graphics），可缩放矢量图形，是一种描述给予二维的矢量图形的基于XML的标记语言。

SVG图片的特点是缩放后不会出现锯齿这样的失真现象。

### 元素

#### 图形元素

1. rect

   x, y, width, height, rx, ry

2. circle

   cx, cy, r

3. line

   x1, y1, x2, y2

4. polyline

   points="0,0 10,10 10,0"

5. polygon

   points=="0,0 10,10 10,0"

6. ellipse

   cx, cy, rx, ry

7. path

   d, [pathLength]( https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/pathLength )（会根据这个设置值和图形路径实际长度来进行缩放，circle等路径图形也支持这个属性）

8. image

   x, y, width, height, xlink:href, preserveAspectRatio（控制图像比例）

9. text

   x, y, dx, dy, text-anchor, rotate, textLength, lengthAdjust, dominant-baseline, alignment-baseline

   - tspan

     用作text元素的子元素，拥有相同的属性

   - textPath

     根据path元素的形状来放置文字。

     xlink:href, startOffset, spacing, method

#### 其他元素

1. svg

   可以作为根元素，也可以内嵌在当前svg文档中，拥有独立视口和坐标系统。

   version, x, y, width, height, preserveAspectRatio, viewBox, xmlns="http://www/w3/org/2000/svg"

2. g

   是用来组合对象的容器，添加到g元素上的属性会被其所有的子元素继承。

3. foreignObject

   用来包含不同XML命名空间的内容，一般是HTML元素。

   x, y, width, height 可以是值或百分比

4. a

   xlink:href, target

5. defs

   用来容纳重复使用的图形元素，主要是出于易读性和可访问性。

6. use

   x, y, width, height, xlink:href

   在SVG文档内取得目标节点，并在别的地方复制它们。依旧可以设置样式。

7. mask

   定义一个透明遮罩层和当前对象合成，形成背景。可以是任何其他图形对象或g元素。使用`mask="url(#id)"`属性来引用

   id, x, y, width, height, maskUnits, maskContentUnits

8. symbol

   用于定义一个图形模板对象，通过use元素来实例化进行展示，自身并不展示。主要是为了添加结构和语义。

   id, viexBox, preserveAspectRatio

9. pattern

   让预定义图形能够以固定间隔在x轴和y轴上重复（或平铺）从而覆盖要涂色的区域。结合`fill="url(#id)"`和`stroke`使用。

   id, x, y, width, height, patternUnits, patternContentUnits, patternTransform, preserveAspectRatio, xlink:href

10. clipPath

    指定可绘制区域，超出区域的部分不会被绘制。被剪切掉的区域外是不响应鼠标事件的。

    其他元素通过`clip-path`属性来引用clipPath元素的id

    id, clipPathUnits

11. marker

    定义在特定的path元素、line元素、polyline或polygon元素上绘制的箭头或多边形标记图形。通过`marker-end="url(#id)"`、`marker-start`、`marker-mid`属性引用。

    id, refX, refY, markerWidth, markerHeight, orient, markerUnits, viewBox

12. title

    鼠标悬浮时的提示性文本，提高可访问性。通常必须是它父元素的第一个子元素时才有作用。只能是纯文本。

13. linearGradient 线性渐变

    x1, y1, x2, y2, spreadMethod, gradientUnits, gradientTransform, xlink:href

14. radialGradient 径向渐变

    id, cx, cy, r, fx, fy, fr, gradientUnits, gradientTransform, spreadMethod, xlink:href

15. stop

    linearGradient或radialGradient的子元素，用于定义渐变中的颜色节点

    offset, stop-color, stop-opacity

16. style 内联样式表，和html的style用法一致

17. filter 滤镜元素

18. animate 动画元素

    放在形状元素的内部，用来定义一个元素的某个属性如何踩着时间点改变。在指定持续时间里，属性从开始值变成结束值。

    attributeName, attributeType, from, to, dur, repeatCount

    ```SVG
    <rect x="10" y="10" width="100" height="100">
        <animate attributeType="XML" attributeName="x" from="-100" to="100" dur="10s" repeatCount="indefinite">
    </rect>
    ```

    

### 属性

1. fill、fill-opacity

2. stroke、stroke-opacity、stroke-width、stroke-dasharray、stroke-linecap、stroke-linejoin、stroke-dashoffset、stroke-miterlimit

3. transform

4. viewBox

   定义视口的位置和大小，配合preserveAspectRatio使用，实现绘图时基于viewBox视口大小绘图，基于preserveAspectRatio规则缩放、裁剪以适应实际容器的大小。`viewBox="min-x min-y width height"`

   适用元素：svg、symbol、marker、pattern、view

5. [preserveAspectRatio](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/preserveAspectRatio )

    用于指示带有`viewBox`的元素按照怎样的缩放方式去适应其可见视窗（viewport）。如果元素没有设置viewBox属性，那么它的preserveAspectRatio属性无效（image元素除外）。

   适用元素：svg、symbol、image、marker、pattern、view、feImage

    语法：`preserveAspectRatio="<align> [<meetOrSlice>]"`

   - align的取值：`none`、(xMin|xMid|xMax)(YMin|YMid|YMax) 9种组合，如`xMidYMid`；`none`时会使缩放元素内容使元素边界完全匹配可见视窗，而且会忽略meetOrSlice的值。
   - meetOrSlice：可选，`meet`（默认），保留图形宽高比，使整个viewBox在视口范围内可见，满足其他条件的情况下尽可能地放大元素的viewBox；`slice`，保留图形宽高比，整个视口范围被viewBox覆盖，满足其他条件情况下尽可能缩小viewBox。

6. clip-path 裁切

   clip-path="url(#id)"

### Path命令

1. M、m  移动至

2. L、l  画线至

3. H、h  水平画线至

4. V、v  垂直画线至

5. Z、z  结束路径

6. A、a  绘制弧线

    `A rx ry x-axis-rotation large-arc-flag sweep-flag x y` 

   `a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy`

   x-axis-rotation表示弧形的旋转情况，在屏幕2d层面的顺时针旋转；

   large-arc-flag表示绘制大角度弧还是小角度弧，0表示小角度，1表示大角度；

   sweep-flag表示弧线的方向，0表示从起点到终点沿逆时针画弧，1表示从起点到终点沿顺时针画弧。

7. C、c  三次贝塞尔曲线

   `C x1 y1, x2 y2, x y`

   `c dx1 dy1, dx2 dy2, dx dy`

   (x1, y1)、(x2, y2)是控制点，(x, y)是终点。

   控制点描述的是曲线起始点的斜率，曲线上各个点的斜率，是从起点斜率到终点斜率的渐变过程。

8. S、s  简写三次贝塞尔曲线

   `S x2 y2, x y`

   `s dx2 dy2, dx dy`

   如果S命令跟在一个C或S命令后面，则它的第一个控制点会被假设成前一个命令曲线的第二个控制点的中心对称点。如果S命令单独使用，前面没有C或S命令，那么当前点将作为第一个控制点，这时候相当于Q命令。

9. Q、q  二次贝塞尔曲线

   `Q x1 y1, x y`

   `q dx1 dy1, dx dy`

   (x1, y1)是控制点，(x, y)是终点。

10. T、t  简写二次贝塞尔曲线

    `T x y`

    `t dx dy`

    T命令前是Q或T命令时，会和S命令一样推断其控制点；如果单独使用，那么画出来的会是一条直线。

### 接口

1. ` SVGGraphicsElement.getBBox()`：计算元素相对于其当前所在SVG空间的坐标边界，返回结果是一个SVGRect对象，包含`x`、`y`、`width`、`height`属性。
2. ` SVGGeometryElement.getTotalLength()`：返回路径长度的计算值，path、circle等元素都适用
3. ` SVGGeometryElement.getPointAtLength(float distance) `：返回路径上相应距离的点的坐标，是一个SVGPoint对象，包含x、y属性。
4. HTML的`getComputedStyle(element)`、`element.getBoundingClientRect()`等方法同样支持SVG元素，前者可以同样计算SVG的特定属性，如x、y等，后者类似`getBBox`，但参照的坐标系不一样，`getBBox`是参照元素所属SVG的坐标系，`getBoundingClientRect`是相对于浏览器视口的（首受页面滚动影响）。
5. 创建SVG元素需要使用`document.createElementNS(svgNamespaceURI, type)`，svg的命名空间为**http://www.w3.org/2000/svg**，可以使用`elem.namespaceURI`来访问以确认，如果命名空间错误会导致无法识别为SVG元素；增加子元素依旧使用`appendChild`等；设置属性使用`element.setAttributeNS(null | namespaceURI, attr, value)`，不过大部分情况依旧可以使用`element.setAttribute(attr, value)`。

### SVG2

1. 移除了xlink命名空间（不知道支持性怎么样）

   >  **Note:** SVG 2 removed the need for the `xlink` namespace, so instead of `xlink:href` you should use `href`. 

### 参考资料

1. [SVG——MDN]( https://developer.mozilla.org/zh-CN/docs/Web/SVG )

