## JavaScript

1. 数据类型

   - 6种基础类型：null、undefined、number、string、boolean、symbol
   - 引用类型：object
   - 值传递和引用传递区别
   - 函数参数传递
   - typeof
   - instanceof 原理与实现

2. 闭包

   - 含义、原理
   - 应用场景
   - 优缺点

3. ES6+ [《ECMAScript 6入门》 —— 阮一峰]( https://es6.ruanyifeng.com/#README  )

   - let、const
   - 变量的解构赋值
   - 字符串的扩展、新增方法
   - 正则的扩展
   - 数值的扩展
   - 函数的扩展
   - 数组的扩展
   - 对象的扩展、新增方法
   - Symbol
   - Set和Map数据结构
   - Proxy
   - Reflect
   - Promise对象
   - Iterator和for..of循环
   - Generator
   - async/await
   - Class
   - 模块化 import/export
   - 修饰器Decorator

4. this指向

   - 箭头函数
   - bind、call、apply

5. 异步

   - setTimeout/setInterval

   - Promise
   - generator
   - async/await
   - 区别

6. 事件循环

   - 异步
   - 单线程

   - 任务队列、宏任务、微任务

7. DOM事件

   - DOM 0级: onclick = function(){}
   - ~~DOM 1级：没有定义事件相关内容~~
   - DOM 2级：addEventListener / removeEventListener，IE的attachEvent
   - DOM 3级：添加了很多事件类型，焦点事件、鼠标事件、滚动事件等
   - 事件捕获和冒泡：捕获阶段、目标阶段、冒泡阶段
   - 事件代理

8. 原型与原型链

   - 几种继承方式
   - 隐式和显式
   - 构造函数
   - new操作

9. 作用域

   - 全局/局部/块级作用域
   - 作用域链
   - 变量、函数提升

10. 垃圾回收机制 [MDN-内存管理]( https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management )

    - 内存声明周期

    - 内存泄漏
    - 引用计数（旧方案）
    - 标记清除

## 浏览器相关

1. 浏览器渲染原理

   * DNS解析、资源加载、DOM树、渲染树等

   - CSS资源加载是否会阻塞HTML解析和渲染？
   - script脚本资源的async、defer属性
   - load事件和DOMContentLoaded事件

2. cookie

3. 本地缓存

   - localStorage
   - sessionStorage
   - IndexedDB

4. 浏览器缓存

   - 强缓存
   - 协商缓存
   - 相关请求头

5. 浏览器请求

   - http、http2、https，https加密原理
   - tcp
   - 常用请求头
   - 常用content-type
   - ajax，XMLHttpRequest
   - fetch
   - axios库
   - 跨域，jsonp，cors，浏览器同源策略
   - 状态码：302，400，401，500

6. 浏览器安全

   - xss 跨站脚本攻击
   - csrf 跨站请求伪造

## React

1. 生命周期
2. 组件间通信
3. setState
4. 函数组件、类组件、高阶组件、纯组件（PureComponent）
5. children对象和API
6. 虚拟DOM
   - React.createElement
   - diff算法
7. 单向数据流
   - 双向绑定，区别
8. 和Vue的对比
9. 状态管理
   - setState
   - Redux
   - MobX
10. MobX原理
    - 如何触发React组件更新的
    - Object.defineProperty和Proxy区别
11. 路由
    - React-Router
    - 路由实现原理
    - hash路由、history.pushState
12. 组件库
    - AntD
13. hooks
    - useState
    - useEffect
14. React DOM的API
15. SSR服务端渲染的原理

## 工程化构建

1. 模块化

   - 立即执行函数

   - commonjs：module.exports / require
   - ES6：import / export
   - AMD / CMD，require.js
   - 区别

2. webpack

   - 主要配置项
   - loader和plugin区别
   - 常用loader、loader执行顺序
   - 常用plugin

3. TypeScript

   - JavaScript超集
   - 意义
   - 类型
   - 泛型

4. 性能优化

   - 首屏优化
   - 图片优化、雪碧图、base64、webp
   - 压缩、合并
   - 懒加载
   - gzip
   - cdn

## HTML & CSS

1. html5特点

   - doctype
   - 新增元素
   - 语义化
   - audio、video

2. CSS常见布局

3. CSS定位：position

4. 盒模型

5. float

6. flexbox

7. grid

8. 多列布局 column-count

9. 选择器

   - 优先级

   - 伪类
   - 伪元素

   - id、class、标签选择器
   - 属性选择器
   - 子元素选择器、后代选择器
   - 兄弟元素选择器

10. 单行文本省略、多行文本省略

11. CSS动画：transition、animation、@keyframes

12. 媒体查询

13. BFC 块级格式化上下文

14. margin、padding的百分比计算方式

## Nodejs

1. 应用场景：node服务、工具、爬虫等
2. 和写浏览器端js的区别
3. 主要模块
4. express
5. koa，常用中间件
6. nginx，反向代理
7. 数据库：MySQL、MongoDB

## 可视化

1. d3js
   - 主要功能模块
   - update/enter/exit 更新模式
   - selection.data() 数据绑定
2. Echarts、AntV（g2、f2、g6）
3. SVG
   - 图形元素和path路径
   - viewport
   - 动画
4. canvas
   - 主要API
   - 事件交互
   - 动画，requestAnimationFrame
5. SVG和canvas对比
6. 3D可视化
   - WebGL：着色器语言（GLSL）、顶点着色器、片元着色器
   - Threejs：场景、相机、物体（几何体、材质）、渲染器
   - DeckGL、MapboxGL
   - 实用场景：空间相关，家居等室内场景还原、三维地理展示、WebVR
7. 地图
   - GeoJSON
   - TopoJSON
   - 投影算法
   - 地图应用：高德地图、百度地图

## 未分类

1. 多端开发

   - PC端开发和移动端开发的区别

   - React Native
   - Electron
   - Flutter
   - 小程序（微信小程序、支付宝小程序）
   - Weex、uniapp、Taro、Chamelon 

2. 防抖和节流

3. PWA 渐进式Web应用

   - manifest.json
   - Service Worker
   - Push API

4. 函数式编程

   - 函数是一等公民
   - 纯函数
   - 柯里化
   - 偏函数

5. 文件下载、上传实现

6. 图片预览实现

7. 浅拷贝和深拷贝

8. 设计模式

   - 工厂模式
   - 单例模式

   - 装饰器模式
   - 发布-订阅模式
   - 等...

9. 数据结构和算法

   - 排序算法
   - 

10. BigInt

11. 手写实现

    - new操作符
    - instanceof
    - bind、call、apply
    - 数组方法
    - Promise

12. 数组去重方式

13. 国际化 i18n