## HTML

### 1.click 在 ios 上有 300ms 延迟，原因及如何解决？

- 使用meta viewport，将user-scalable设置为no，即禁用双击缩放的功能
- 使用 FastClick 插件

### 2.HTML5 新特性

- 语义化标签
  - nav
  - article
  - footer
  - header
- 媒体标签
  - audio
  - video
- 数据存储
  - sessionStorge
  - localStorge

### 3.src和href的区别

- src表示对资源的引用，当浏览器解析该元素时，会暂停对其它资源的下载和处理，直到将src对应的资源下载、加载、执行完毕，所以一般将script放在文档的底部
- href表示对超链接的引用，当浏览器解析到该元素时，会并行地加载对应的资源，不会停止对文档的处理，一般放在a标签或者link标签中

### 4. script标签中defer和async的区别

- 都是异步加载js文件，不会阻塞后面的加载
- 区别在于多个带有async的标签不能保证加载的顺序，而多个带有defer的标签可以保证加载的顺序

### 5.DOCTYPE(⽂档类型) 的作⽤

DOCTYPE放在文档的开头，告诉浏览器用什么方式加载html

一般分为严格模式和混杂模式

严格模式即要求浏览器按照严格的标准执行页面排版和js；

混杂模式则是向后兼容，防止旧版本的浏览器无法兼容页面



## CSS

### 1.如何画一个三角形

```css
#tri {
    display: inline-block;
    width: 0;
    height: 0;
    border-left: 10px solid transparent;
    border-right: 10px solid transparent;
    border-bottom: 20px solid red;
}
```



### 2.CSS3新特性

- border-radius
- box-shadow
- transform
- animation

### 3.CSS盒模型

css盒模型就是dom元素显示在页面上一块区域。

一般可分为 标准W3C盒子模型和IE盒子模型。

另外，可以通过设置 box-sizing 来切换盒子模型。

- 标准盒模型的width和height只包含content
- 而IE盒模型的width和height包含content、padding和border

box-sizing有三个属性可以选择：content-box（标准盒模型）、border-box（IE盒模型）、padding-box

### 4.画一条0.5px的线

移动端

```css
<meta name='viewport' content='width=device-width, initial-scale=0.5 maximum-scale=0.5 minimum-scale=0.5' >
```

其它

```css
.line {
    transform: scaleY(0.5);
}
```



### 5.link标签和@import标签区别

- link标签属于html标签，而@import属于CSS导入样式的范畴
- 用link标签导入css样式，会在加载页面的同时加载文件，而用@import导入样式会等到页面加载完成之后，再加载文件
- link标签没有兼容性的问题，而@import不兼容低版本的浏览器

### 6.transition 和 animation 的区别

- transition需要事件触发，而animation不需要事件触发，可以自动执行
- transition需要设置两个关键帧，一个开始关键帧和一个结束关键帧；而animation可以使用@keyframe 设置多个关键帧

### 7.Flex 布局

容器属性：

- flex-direction: row || row-reverse || column || column-reverse
- flex-wrap: wrap || no-wrap || wrap-reverse
- flex-flow: <flex-direction> || <flex-wrap>
- justify-content: center || space-around || space-between ...
- align-items: (一行)
- align-content: （多行）

元素属性：

- order
- flex-grow
- flex-shrink
- flex-basis
- flex
- align-self

### 8.BFC

BFC: 块级格式上下文

特点：

1. 同一个 BFC 的相邻两个 box 的外边距会折叠
2. BFC 不会和 float box 发生重叠
3. BFC 中的子元素的布局不会影响到 BFC 外的元素布局
4. BFC 计算高度时会将 float box 计算在内

创建：

1. 根元素 html，本身是一个 BFC
2. float: left || right
3. position: absolute || fixed
4. display: inline-block || table-cell || flex
5. overflow: hidden || scroll || auto

作用：

1. 防止外边距折叠
2. 自适应两栏布局
3. 清除浮动的影响

### 9.垂直居中的方法

1. margin: auto

   ```css
       .container {
         width: 300px;
         height: 400px;
         border: 1px solid red;
         position: relative;
       }
       .box {
         width: 10px;
         height: 10px;
         background-color: red;
         position: absolute;
         left: 0;
         right: 0;
         top: 0;
         bottom: 0;
         margin: auto;
       }
   ```

   

2. translateY

   ```css
       .container {
         width: 300px;
         height: 400px;
         border: 1px solid red;
         position: relative;
       }
       .box {
         width: 10px;
         height: 10px;
         background-color: red;
         position: absolute;
         left: 50%;
         top: 50%;
         transform: translate(-50%, -50%);
       }
   ```

   

3. flex

   ```css
       .container {
         width: 300px;
         height: 400px;
         border: 1px solid red;
         display: flex;
         justify-content: center;
         align-items: center;
       }
       .box {
         width: 10px;
         height: 10px;
         background-color: red;
       }
   ```

4. table-cell

   ```css
       .container {
         width: 300px;
         height: 400px;
         border: 1px solid red;
         display: table-cell;
         vertical-align: middle;
       }
       .box {
         width: 10px;
         height: 10px;
         background-color: red;
       }
   ```

   

### 10.块元素和行内元素

块元素：

- 元素会独占一行
- 可以设置width、height、margin、padding等属性

行内元素：

- 元素不会独占一行
- 不可以设置width、height，而且垂直方向的margin、padding无效



### 11.单行和多行文本省略号

- 单行

  ```css
  div {
      white-space: no-wrap;  // 文本不换行
      overflow: hidden;  // 隐藏溢出
      text-overflow: ellipsis; // 文本溢出显示省略号
  }
  ```

- 多行

  ```css
  div {
      display: -webkit-box; // 作为弹性伸缩盒子显示
      -webkit-box-orient: vertical; // 设置伸缩盒子中子元素排列方式：从上到下垂直排列
      -webkit-line-clamp: 3; // 显示行数
      overflow: hidden;
  }
  ```

  

### 12.visibility=hidden、opacity=0、display：none

- opacity=0
  - 将元素的不透明度设置为0，元素依然占据空间，而且会触发事件的监听函数、
- visibility=hidden
  - 元素依然占据空间，但不会触发事件的监听函数
- display：none
  - 渲染树中不包含该元素，所以元素不占据空间，也不会触发响应函数

### 13.外边距折叠

同一个 BFC 中两个相邻的元素会产生外边距折叠的现象。

- 如果两个元素的margin 值同为正数或同为负数，那么会取绝对值更大的margin作为外边距
- 如果两个元素的margin 值为一正一负，那么会取两者之和作为外边距

### 14.position

- static，默认，出现在正常的文档流中，没有left、right、top、bottom
- relative 相对定位，相对元素本身的位置进行偏移
- absolute 绝对定位，相对离自己最近的已定位的父元素进行定位，如果祖先元素都没有定位，则相对html
- fixed 固定定位
- sticky 粘滞定位
- inherit 继承父元素的定位

### 15.清除浮动

1. 创建 BFC。将父元素设为 `overflow: hidden;` 使之成为一个 BFC，会计算浮动元素的高度

2. 使用 clear

   ```css
   .clearfix::after {
       content: '';
       clear: both;
       display: table;
   }
   ```

   

### 16.CSS选择器、优先级

选择器：id选择器、类选择器、伪类选择器、属性选择器、标签选择器、伪元素选择器、通配选择器...

优先级：!import > style内联样式 > id选择器 > 类选择器、伪类选择器、属性选择器 > 标签选择器、伪元素选择器 > 通配选择器 > 浏览器默认样式  

### 17.自适应两栏布局、圣杯布局（三栏）

### 18.calc

计算值，运算的两边必须添加空格

### 19.预处理器

- less
- sass

### 20.对requestAnimationframe的理解

requestAnimationframe 告诉浏览器要执行一个动画，并且浏览器要在下一次重绘之前，调用指定的回调函数来更新动画。

它需要传入一个函数，该回调函数会在浏览器下一次重绘之前执行。

相比于使用 setTimeout 或 setInterval 来实现动画效果，使用 requestAnimationframe 可以降低cpu的消耗，对函数节流并且可以减少DOM操作。

### 21.Canvas和SVG的区别

SVG即可缩放矢量图形(scalable vector graphic) ，它是基于可扩展标记语言XML描述的2D图形语言，因此每个SVG都可以显示，而且可以表示为一个对象，当对象的属性发生变化，浏览器能够自动重绘图形。

特点：

1. 不依赖分辨率
2. 支持JavaScript事件处理器
3. 适合带有大型渲染区域的应用，如谷歌地图
4. 复杂度高而且会减慢渲染速度
5. 不适合游戏应用

Canvas 指画布，它是用JavaScript来绘制2D图形，而且是逐像素进行渲染的，一旦位置发生改变，就会重新绘制图形。

特点：

1. 依赖分辨率
2. 不支持JavaScript事件处理器
3. 弱的文本渲染能力
4. 能够以 .png 或 .jpg 的格式保存结果图形
5. 适合图像密集的游戏应用

### 22.阐述一下 CSSSprites

即css精灵图，是指将多张图片合并到一张大图中，然后通过 background-image、background-repeat、background-position 进行背景的定位。

可以减少页面的http请求数，提高网页的加载速度。

### 23.常见的CSS布局单位

- px：分为css像素和物理像素
- %：一般相对于直接父元素
- rem：相对于html中的font-size
- em：相对于当前元素中的font-size
- vw：相对于视口的宽度
- vh：相对于视口的高度

### 24.两栏布局的实现

1. float

   ```css
   .left {
   	width: 100px;
       float: left;
       height: 300px;
     	background-color: red;
   }
   .right {
       overflow: hidden;
       height: 300px;
       background-color: green;
   }
   ```

2. flex

   ```css
   .container {
       display: flex;
       height: 300px;
   }
   .left {
       width: 100px;
       background-color: red;
   }
   .right {
       flex: 1;
       backgroud-color: green;
   }
   ```

### 25..三栏布局的实现

1. absolute

   ```css
   .container {
       position: relative;
   }
   .left {
       position: absolute;
       width: 100px;
       height: 300px;
       background-color: green;
   }
   .center {
       height: 300px;
       background-color: blue;
       margin: 0 100px;
   }
   .right {
       width: 100px;
       height: 300px;
       background-color: red;
       position: absolute;
       top: 0;
       right: 0;
   }
   ```

2. flex

   ```css
       .container {
         display: flex;
       }
       .left {
         flex: 0 0 100px;
         height: 300px;
         background-color: greenyellow;
       }
       .right {
         flex: 0 0 200px;
         height: 300px;
         background-color: grey;
       }
       .middle {
         flex: 1;
         height: 300px;
         background-color: red;
       }
   ```

3. float（这种方法必须要将右栏放到中栏的上面）

   ```html
     <style>
       * {
         margin: 0;
         padding: 0;
       }
       .left {
         float: left;
         height: 300px;
         width: 100px;
         background-color: grey;
       }
       .middle {
         height: 300px;
         background-color: red;
         margin-left: 100px;
         margin-right: 200px;
       }
       .right {
         width: 200px;
         height: 300px;
         background-color: green;
         float: right;
       }
       
     </style>
   </head>
   <body>
     <div class="container">
       <div class="left"></div>
       <div class="right"></div>
       <div class="middle"></div>
     </div>
   </body>
   ```

### 26.实现一个扇形

```css
.box {
    width: 0;
    height: 0;
    border: 100px solid transparent;
    border-radius: 100px;
    border-top-color: red;
}
```

### 27.实现一个宽高自适应的正方形

```css
.box {
    width: 20%;
    height: 0;
    padding-top: 20%;
    background-color: red;
}
```



---

## JavaScript

### 数据类型

基本数据类型：

- Number
- String
- Boolean
- null
- undefined
- BigInt (ES6)
- Symbol (ES6)

引用数据类型：

- Function
- Object
- Array
- Date

### 数据类型检测

1. typeof

   基本能检测大部分数据类型，有两个例外：

   - null  -->  'object'
   - Array  -->  'object'

2. instanceof

   - 只能检测引用数据类型
   - 本质上是查找实例原型链中是否有类型的原型对象

3. construtor

   - 不能检测 null 和 undefined 类型
   - 如果构造函数改变了原型对象，就不能通过这种方法判断了

4. Object.prototype.toString.call()

   基本上可以判断所有数据类型

5. Array.isArray()

   ES6语法，用于判断数组

6. isNaN()  /  Number.isNaN()

   判断是否为 NaN，后者更为精确，不会将数据转为number

### Object.is() 与 “===”、“==” 

- === 不会发生类型转换
- == 会发生类型转换
- Object.is() 和 === 类似，不过有一些特殊情况，比如 +0 和 -0 不再相等，NaN 和 NaN 相等

###  let、const、var的区别

`块变挂重暂初指`

1. 块级作用域
2. 变量提升
3. 挂载到全局变量
4. 重复声明
5. 暂时性死区（在使用let、const命令声明变量之前，该变量都是不可用的。这在语法上，称为**暂时性死区**。使用var声明的变量不存在暂时性死区。）
6. 初始值设置
7. 指针指向修改

### 箭头函数与普通函数的区别

- 箭头函数更加简洁
- 箭头函数没有 this
- 箭头函数没有 arguments

### Proxy

Proxy 是一个构造函数，需要传入两个参数：target 和 handler。它可以构造出代理对象，这个代理对象可以代理目标对象 target 做一些事，当执行某个操作时，它会执行 handler 所对应的函数。

handler 中常见的拦截方法有 get、set、has、deleteProperty等13种方法。

### 作用域

作用域是定义变量的区域，它有一套访问变量的规则，通过这套规则可以访问到代码内各个区域内的变量。作用域又分为全局作用域、函数作用域还有块级作用域。查找变量时，会从当前作用域中查找该变量，如果找不到就从父级作用域中查找，这样一层层从内到外查找变量，直到全局作用域，这种变量查找的次序就叫做作用域链。

### 创建对象的方式

1. 字面量模式

   {}创建，简单方便，但要创建多个对象时，代码冗余。

2. 工厂函数模式

   用函数封装创建对象的细节，但只是复用了代码，没有建立起对象和类型之间的联系。

3. 构造函数模式

   每一个函数都是构造函数，可以通过new来调用。缺点是如果对象中包含函数，那么每一个创建的对象中都要相同的函数空间，浪费了不必要的内存空间。

4. 原型模式

   可以向构造函数的原型对象中添加公用属性和方法，缺点就是如果是引用类型的话比如Array，那么所有的对象实例都会共用引用类型的内存，容易造成数据的篡改。

5. 构造函数 + 原型模式

   组合了构造函数模式和原型模式，通过构造函数模式可以初始化一些基本类型的属性和方法，利用原型模式设置对象的公共方法。

### 继承的方式

1. 原型链继承

   子类构造函数的原型对象指向父类构造函数的实例。

   缺点：

   - 在包含有引用类型的数据时，会被所有实例共享，容易造成数据的篡改。
   - 创建子类型时不能向父类型传递参数。

2. 构造函数继承

   在子类构造函数中调用父类构造函数，解决了子类不能向父类传递参数的问题。

   缺点：不能继承父类原型对象中的属性和方法。

3. 组合继承

   结合了原型链继承和构造函数继承。

   缺点是整个过程调用了两次父类的构造函数，会在子类的原型对象和实例对象中创建两份相同的属性或方法。

4. 寄生组合继承

   是组合继承的改进，寄生组合继承创建了父类原型对象的副本，将子类的原型对象指向了这个副本，从而避免了属性或方法的重复。

5. class的extends继承

   extends后面加上父类class的形式继承，通常需要在constructor中调用super函数，完成对父类数据的初始化。

### 原型、原型链

在 JS 中可以通过构造函数来创建对象，每个构造函数都有一个 prototype 属性，这个 prototype 指向的一个 Object 对象，也叫做原型对象，可以向原型对象里面添加公用的属性和方法，所有实例都会共享这些属性和方法。另外，prototype 属性中还有一个 constructor 属性，指向了构造函数。

所有实例对象中都会有一个 \__proto\__ 属性，它指向的是构造函数的原型对象，当我们在实例中查找属性时，如果在当前实例中找不到该属性，就会到 \__proto\__ 指向的内存中查找，如果找不到，就会再去 \__proto\__ 中找，直到 \__proto\__ 为空，这也就叫做原型链，查找变量时会顺着这条原型链一层层往上找。

### 闭包

闭包是指有权访问另一个函数作用域中变量的函数，形成闭包需要两个条件：在函数内创建一个嵌套函数、嵌套函数有对外部函数变量的引用。

闭包有两个常用的作用：

- 使函数外部可以访问到函数内部的变量，可以创建私有变量。
- 使函数执行完之后，函数内部的变量不会立马被销毁，而是留在内存中。

### Iterator Generator

Iterator 为各种数据结构提供一个统一的、简便的访问接口，主要用于 ES6 中的 for...of 循环。

当给一个对象添加 `[Symbol.iterator]` 属性后，对象就会变为可迭代对象，就可以使用 for...of 遍历。

这个属性是一个函数，函数必须返回一个对象，这个对象必须包含一个 next 函数，next 函数必须返回一个对象，这个对象必须要有 value 和 done 两个字段，value 表示当前遍历的值，done 表示是否遍历完。

Generator 函数可以说是 Iterator 接口的具体实现方式。可以通过 yield 代替 返回的 next 函数，更加简便。

```js
const person = {
  info: {
    name: 'John',
    gender: 'male',
    address: 'beijing',
    age: 18
  }
}

// 使用普通函数构造迭代器
person[Symbol.iterator] = function() {
  let info = this.info
  let keys = Reflect.ownKeys(info) // 键名
  let index = 0 // 指针索引
  return {
    next() {
      if (index < keys.length) {
        return {
          done: false, // 是否遍历完成
          value: info[keys[index++]] // 当前值
        }
      } else {
        return {
          done: true,
          value: undefined
        }
      }
    }
  }
}

// 使用Generator构造迭代器
person[Symbol.iterator] = function * () {
  let info = this.info
  let keys = Reflect.ownKeys(info)
  let index = 0
  while (true) {
    if (index < keys.length) {
      yield info[keys[index++]] // 相当于next函数
    } else {
      return false
    }
  }
}

for (let i of person) {
  console.log(i); 
  // John
  // male
  // beijing
  // 18
}
```



### 1.get 请求传参长度的误区

### 2.来讲讲 JS 的闭包吧

### 3.继承

### 4.解决异步回调地狱

### 5.前端中的事件流

### 6.如何让事件先冒泡后捕获

### 7.说一下事件委托

### 8.说一下图片的懒加载和预加载

### 9.mouseover 和 mouseenter 的区别

### 10.JS 的 new 操作符做了哪些事情

### 11.bind，apply，call 的区别

### 12.JS 的各种位置，比如 clientHeight,scrollHeight,offsetHeight ,以及 scrollTop, offsetTop,clientTop 的区别？

### 13.异步加载 JS 的方法

### 14.JS 的节流和防抖

### 15.JS 中的垃圾回收机制

### 16.eval 是做什么的

### 17.如何理解前端模块化

### 18.说一下 CommonJS、AMD 和 CMD

### 19.深浅克隆

### 20.JS 监听对象属性的改变

### 21.==和===、以及 Object.is 的区别

### 22.setTimeout、setInterval 和 requestAnimationFrame 之间的区别

### 23.JS 怎么控制一次加载一张图片，加载完后再加载下一张

### 24.Function._proto_(getPrototypeOf)是什么？

### 25.JS 判断类型

### 26.数组常用方法

### 27.数组去重

### 28.能来讲讲 JS 的语言特性吗

### 29.JS 实现跨域

### 30.JS 基本数据类型

### 31.this 的指向 哪几种

## Vue

### 1.有使用过 Vue 吗？说说你对 Vue 的理解

### 2.说说 Vue 的优缺点

### 3.什么是虚拟 DOM？优缺点？

虚拟DOM本质上是一个JavaScript对象，是对真实DOM抽象，当状态发生变化时，会记录新的DOM树和旧的DOM树的差异，最后把差异更新到真正的DOM中。

优点：

1. 提高性能
2. 无需手动操作DOM
3. 跨平台

缺点：

- 无法进行极致优化

- 首次加载大量DOM的时候，由于多了一层虚拟DOM运算，所以会比innerHTML插入更慢

### 4.请描述下 vue 的生命周期是什么？

vue 的生命周期涉及到八个钩子函数。

- beforeCreate
  - 初始化事件和生命周期
  - el、data、methods 未初始化，无法获取vue实例的属性和方法
  - 一般我们会在加上一个 loading 事件，提示用户正在加载
- created
  - 完成了数据观测、属性和方法的计算、watch事件的回调
  - 但是挂载还没有开始，无法获取到dom元素
  - 一般我们会在这里进行初始数据获取，比如向服务器发送请求
- beforeMount
  - 主要是获取编译的模板
  - 首先会判断vue实例有没有el选项，如果没有就会停止编译，直到用户输入$mount
  - 然后会判断vue实例有没有template选项，如果有，就将template作为模板编译成render函数，如果没有，就将外部的HTML作为编译模板
- mounted
  - 这个阶段主要是给vue实例对象添加$el 成员，并且用beforeMount获取到的编译模板替换挂载的DOM，将data中的数据渲染到占位符中
  - 一般在这个阶段会拿回向后端请求的数据，并配合其它的钩子函数完成一些事情
- beforeUpdate
  - 当渲染到页面的数据发生改变时，就会触发这个钩子函数
- updated
  - 当渲染到页面的数据发生改变并且修改后的数据渲染到视图层之后，才会触发这个钩子函数
- beforeDestroy
  - 当用户调用$destroy方法，会触发这个钩子函数
  - 在这个阶段，vue实例仍然可用
  - 一般会在这个阶段，会进行一些善后操作，比如清除计时器
- Destroyed
  - 在这个阶段，vue会卸载watcher、事件监听和子组件
  - 此时DOM元素仍然存在，只是不再受vue控制

### 5.watch 怎么深度监听对象变化

### 6.删除数组用 delete 和 Vue.delete 有什么区别？

### 7.watch 和计算属性有什么区别？

### 8.Vue 双向绑定原理

主要设计到两个部分：数据劫持和发布订阅者模式

当我们new一个vue实例的时候，通常会传入两个参数，一个是data，另一个是el

首先，vue会分别将这两个参数传入到observer和compiler中

- 当data传入到observer之后，会遍历data中的各个属性，通过使用Object.defineProperty进行数据劫持，在劫持过程中主要完成三件事，第一是新建一个发布者对象dep，这个对象中包含notify函数，用于通知所有watcher完成数据更新；第二是创建getter，即当获取对象属性时，触发这个getter，从而新建一个watcher，并将其添加到dep中；第三是创建setter，即当设置对象属性时，触发这个setter，从而调用dep对象的notify，通知所有watcher完成数据更新。
- 当el传入到compiler中，compiler会解析每一条指令，将el中的占位符替换并渲染到页面中，完成页面的初始化，此时由于调用了对象属性，所以会触发getter，将watcher绑定到dep中。

### 9.v-model 是什么？有什么用呢？

### 10.说一下 CommonJS、AMD 和 CMD

1. CommonJS 开始是在服务端中使用的，比如 node 就参照了 CommonJS 的规范，在 CommonJS 中，利用 module.exports 导出模块，然后利用 require 加载模块
2. AMD 全称为异步模块定义（Asynchronous Module Definition），它采用异步的方式加载模块，而且相比于 CommonJS，它的 require 语句发生了变化，require 中需要两个参数，第一个参数是[module]，它是一个数组，里面包含要被加载的模块，第二个参数是 callback，表示加载成功之后的回调函数， 通常把依赖加载的语句放在这个回调函数中。
3. CMD 全称为通用模块定义（Common Module Definition），CMD 规范是国内提出来的，它有一套框架叫做 SeaJS，所有模块都用 define 来定义，然后用 require 引入依赖

---

## 计算机网络

### 1.GET和POST的请求的区别

1. Get是一个幂等请求，不会服务器的资源产生影响，而Post不是一个幂等请求，会对服务器的资源产生影响
2. Get请求一般会被浏览器缓存，而Post不会
3. Get请求参数的长度有限制，而Post没有
4. Get参数通过url传递，Post放在 request body 中
5. Get 比 Post 更不安全，因为参数直接暴露在 url 中
6. Get请求只能进行 url 编码，而 Post 支持多种编码

### 2.POST和PUT请求的区别

- PUT请求可以理解为更新数据，不会增加数据的种类，只会修改数据的内容
- POST请求可以理解为创建数据，它会增加数据的种类，因为会创建新的内容

### 3.常见的HTTP请求头和响应头

请求头：

- Accept
- Cookie
- User-Agent
- Connection

响应头：

- Cache-control
- content-type
- Date
- Connection

### 4.常见的HTTP请求方法

- Get
- Post
- Put
- Delete
- Head（用来获取报文首部，但不返回报文主体部分）
- Options（询问支持的请求方法，用来进行跨域请求）

### 5.HTTP 1.0和 HTTP 1.1 之间有哪些区别？

- HTTP1.0默认使用非持久连接，而HTTP1.1默认使用持久连接
- HTTP1.0使用expires作为缓存判断标准，而HTTP1.1引入了Etag等
- HTTP1.1新增了多个请求方法：PUT、HEAD、OPTIONS

### 6.HTTP 1.1和 HTTP 2.0 的区别

- 二进制协议。HTTP2.0是彻底的二进制协议，头信息和数据体都是二进制，而在HTTP1.1中，头信息必须是文本，数据体可以是文本，也可以是二进制。
- 多路复用。HTTP2.0实现了多路复用，在一个TCP连接中，客户端和服务端可以同时发送或接收多个请求或响应，而且不用按照顺序一一发送，这样避免了“队头堵塞”的问题
- 数据流。HTTP2.0引入了数据流的概念，因为HTTP2.0的数据包不按照顺序一一发送，同一个连接里的连续的数据包可能属于不同的请求。因此，会对数据包进行标记，每个请求或者响应对应的所有数据包称为一个数据流。
- 头信息压缩。HTTP2.0引入了头信息压缩机制，能够节省带宽，和提高访问速度
- 服务器推送。HTTP2.0支持在服务器未经允许，主动向客户端发送资源。

### 7.HTTP和HTTPS协议的区别

- HTTPS需要CA证书，费用较高
- HTTP协议是超文本传输协议，信息是明文传输的，而HTTPS是更加安全的SSL加密传输协议
- 两者使用不同的连接方式，使用的端口也不同，HTTP默认使用80端口，而HTTPS默认使用443端口
- HTTP连接简单，而且无状态。HTTPS协议是由HTTP协议和SSL协议共同构建的可以进行加密传输和身份认证的网络协议，更加安全。

### 8.GET方法URL长度限制的原因

IE对URL长度的限制是2083个字节，是所有浏览器中最小的。

所以只要满足URL长度不超过2083个字节，就能够保证在所有浏览器中都不会出现问题。

### 9.当你在浏览器中输入 Google.com 并且按下回车之后发生了什么？

1. 首先浏览器会对URL进行解析，如果URL中的协议名或主机名不合法，就会将它发送给搜索引擎进行搜索。如果合法，就会检查URL中有没有出现非法字符，如果有的话就会进行转义处理。然后再进行下一步。
2. 接下来，浏览器会查看本地的缓存，如果本地缓存中有URL对应的资源，就会直接使用缓存，没有的话就进行下一步。
3. 下一步是将URL中的域名转换为IP地址。首先浏览器会向本地DNS服务器发送请求，本地DNS服务器收到请求之后，会查看服务器中有没有缓存该域名，如果有，就将该域名对应的IP地址返回给浏览器。如果没有，就向根域名服务器发送请求，获取到顶级域名服务器的地址，然后本地DNS服务器就会向顶级域名服务器发送请求，获取权威域名服务器的地址，然后本地DNS服务器就会向权威域名服务器发送请求，权威域名服务器就会将IP地址，返回给本地DNS服务器，本地DNS服务器收到之后，先会将IP地址缓存，然后返回给浏览器。这样浏览器就收到了域名对应的IP地址。
4. 接下来，浏览器还会获取目标主机的MAC地址。首先，会先判断目标主机是否子网内，如果在的话，会使用ARP协议获取到目标主机的MAC地址，如果不在的话，就会使用ARP协议获取对应网关的MAC地址。
5. 然后，客户端和服务端就会通过三次握手，建立TCP连接。
6. 另外，如果协议是HTTPS的话，还会进行TLS的四次握手。首先客户端会向服务端发送协议的版本号、一个随机数和加密方法。服务端收到之后，确认加密方法， 然后向客户端发送一个随机数和数字证书。客户端收到之后，检查数字证书是否有效，如果有效，就再生成一个随机数，然后用数字证书里面的公钥对随机数进行加密，同时提供对之前所有内容的哈希值让服务端检验，然后发送给服务端。服务端收到之后，使用自己的私钥对数据解密，同时向客户端发送之前所有内容的哈希值供客户端检验。这个时候，双方都有三个随机数，按照之前约定的加密方法，使用这三个随机数生成一把密钥，以后双方通信之前，都会使用这个密钥对数据进行加密后传输。
7. 当连接建立好之后，服务端会向客户端发送一个html文件，浏览器会根据html文件渲染页面
8. 首先，浏览器会根据html文件构造出DOM树，然后根据CSS文件构造出CSSOM树，然后通过DOM树和CSSOM树构建渲染树。浏览器会根据渲染树进行布局。布局完成之后，浏览器使用UI接口对页面进行绘制。这个时候，页面就显示出来了。
9. 最后，当数据传送完成之后，会进行四次挥手，释放TCP连接。

### 10.对keep-alive的理解

### 11.页面有多张图片，HTTP是怎样的加载表现，如何解决？

### 12.HTTP协议的优点和缺点

### 13.HTTP状态码

- 1xx 信息性的状态码
  - 100 提示客户端继续请求
  - 101 切换协议
- 2xx 成功状态码
  - 200 请求成功
- 3xx 重定向状态码
  - 301 永久重定向
  - 302 临时重定向
  - 304 资源未修改
- 4xx 客户端错误状态码
  - 400 客户端请求的语法错误
  - 401 用户未认证
  - 403 服务器拒绝执行请求
  - 404 资源未找到
- 5xx 服务端错误状态码
  - 500 服务器内部发生错误

### 14.DNS协议介绍

### 15.OSI七层模型

- 应用层
  - HTTP
  - HTTPS
  - FTP（文件传输协议）百度网盘、迅雷。。。
  - SMTP（简单邮件传输协议）用户邮箱验证登录
- 表示层
- 会话层
- 传输层
  - TCP
  - UDP
- 网络层
  - ARP
  - RARP
- 数据链路层
  - 以太网协议
- 物理层

### 16.TCP/IP五层协议

- 应用层
  - HTTP
  - HTTPS
  - SMTP
  - FTP
  - DNS
- 传输层
  - TCP (Transmission Control Protocol) 传输控制协议
  - UDP (User Datagram Protocol) 用户数据报协议
- 网络层
- 数据链路层
- 物理层

### 17. TCP 和 UDP的概念及特点

1. UDP面向无连接，不需要建立连接就可以发送数据，而TCP面向连接，需要三次握手
2. UDP支持一对多，多对一和多对多的交互通信，而TCP只能一对一通信
3. UDP面向报文，TCP面向字节流
4. UDP传输不可靠，没有拥塞控制和流量控制，而TCP连接可靠，具有拥塞控制和流量控制
5. UDP的首部开销小，只有八个字节，而TCP的首部最小20个字节，最大60个字节
6. UDP使用于实时应用，如视频会议、IP电话、直播等，TCP适用于要求传输可靠的应用，如文件传输。

### 18.UDP协议为什么不可靠？

### 18.TCP的可靠性是如何保证的？

1. 数据包校验
2. 对失序的数据包重新排序
3. 去除重复的数据包
4. 应答机制
5. 超时重发机制
6. 流量控制

### 19.TCP的重传机制

### 20.TCP的拥塞控制机制

### 21. TCP的流量控制机制

### 22.TCP的可靠传输机制

### 23.TCP的三次握手和四次挥手

三次握手：

1. 客户端向服务端发送一个SYN报文，并带上初始化序列号ISN，发送完成之后，客户端处于SYN_SENT状态
2. 服务端收到客户端的SYN报文，也向客户端发送一个SYN报文，并带上初始化序列号ISN，同时会发送一个ACK报文，其中确认号为客户端的初始化序列号加1，此时服务端处于SYN_REVD状态
3. 客户端收到服务端的报文之后，会向服务端发送一个确认报文，确认号为服务端的初始化序列号加1，表示收到了服务端的SYN报文，此时客户端处于ESTABLISHED状态。服务端在收到报文之后，也会处于ESTABLISHED状态，此时双方的连接就建立起来了。

为什么要三次握手？两次不行吗？

主要是因为第三次握手的作用是客户端要让服务端知道它的序列号已经被确认，如果只进行两次握手的话，那么服务端就无法知道自己的序列号有没有被客户端确认。同时，这也是为了防止已经失效的请求报文被服务器接收而出现错误的情况。

举个例子，当客户端发送一个请求给服务端，这个请求因为某些原因在网络中传送了好久也没有到达服务端，那么这时客户端就会重新发送另一个请求，假如第二次请求很快就被服务端接收了，并且双方完成了数据传送，此时如果第一次请求终于到达了服务器，由于只进行两次握手，只要服务端确认报文，连接就算建立了，而客户端由于已经完成了数据传送，就会忽略服务端发来的确认报文，所以就会导致服务端一直处在等待过程中，浪费资源。



四次挥手：

1. 客户端和服务端一开始处于ESTABLISHED状态，当客户端想要释放连接，客户端就会向服务端发送一个FIN报文，并携带了自己的序列号，此时客户端会处于FIN_WAIT1的状态。
2. 当服务端收到报文之后，会向客户端发送一个确认报文，确认号为客户端序列号加1，并且也会携带自己的序列号，此时服务端会处于CLOSE_WAIT的状态。当客户端收到服务端的确认报文之后，就会变为FIN_WAIT2状态。
3. 当服务端想要释放连接时，会向客户端发送一个FIN报文，并且会携带确认号和序列号，此时服务端处于LAST_ACK状态
4. 客户端收到报文之后，同样会发送一个确认报文作为应答，而且确认号的值为服务端序列号的值加1，此时客户端处于TIME_WAIT状态。客户端会等待2MSL时间，如果这段时间内没有收到服务端的重发请求，就会处于CLOSE状态。服务端在收到确认报文之后，会立马变成CLOSE状态。

为什么要进行四次挥手？

主要是因为TCP的连接是全双工的，所以真正断开连接是需要双方都断开连接的。如果只有一方断开连接，只是表示这一方不能向另一方发送数据，而另一方还可以向这一方发送数据，此时连接只是处于半释放的状态。

为什么要等待2MSL秒？

为了防止客户端向服务端发送的请求丢失或者出错，从而导致服务端不能正常关闭。

### 24.WebSocket 是什么

WebSocket是HTML5提供的一种能让客户端和服务端进行全双工通信的网络技术，它属于应用层协议。WebSocket基于HTTP传输协议，并复用了TCP的握手通道，浏览器只要完成一次握手，就可以建立持久性的连接，并且进行双向数据传输。

最大的特点就是服务端能主动向客户端推送消息，客户端也能够向服务端推送消息。

---

## 浏览器原理

### 1.XSS 

XSS全称是跨站脚本攻击，是一种代码注入攻击。攻击者会向网站中注入恶意代码，让它运行在浏览器上，从而获取用户的信息，如Cookie、LocalStorage

本质上是由于网站没有对恶意代码进行过滤，将恶意代码和正常代码混在了一起，从而导致浏览器无法分辨哪些是正常代码。

XSS一般分为存储型、反射性和DOM型。

通过XSS攻击，攻击者可以：

- 获取页面数据，如Cookie、LocalStorage
- 破坏页面结构
- 流量劫持
- 进行DOS攻击，发送合理请求，占用服务器资源，使用户无法访问服务器

防御手段：

- 使用纯前端的方式，不用服务器返回的拼接的HTML
- 对插入HTML中的代码做好充分的转义
- 使用CSP，建立一个白名单，告诉浏览器哪些外部资源可以被加载执行
- 对敏感信息进行保护，如cookie设置为http-only，禁止Javascript获取cookie

### 2.CSRF

CSRF全称为跨站请求伪造攻击。攻击者会诱导用户进入一个第三方网站，该网站会向被攻击的网站发送同源请求，假如用户在被攻击的网站中登录了，则会利用用户的登录状态，跳过后台验证，冒充用户向服务器发送一些请求。

本质上是利用了cookie可以在同源请求中携带发送给服务器的特点，以此实现用户的冒充。

攻击类型：

- GET类型，比如在img标签构建一个请求
- POST类型，比如在构建一个表单，使其自动提交
- 链接类型，比如在a标签里构建一个请求

防御方法：

- 使用同源检测，服务器对http请求头中的origin或者referer进行检测，判断是否为允许访问的网站，从而实现对请求的过滤
- 使用 CSRF Token进行验证
- 使用双重 Cookie 进行验证
- 给 Cookie 设置 Samesite 属性，就是限制 cookie 不能被第三方使用



### 3.进程与线程

### 4.说一说浏览器的缓存机制

- 当浏览器请求资源时，会优先使用强缓存，首先会先计算当前时间和上一次服务器返回200的时间之差，如果时间差没有超过cache-control中的max-age，则会命中强缓存，直接接用本地的资源文件；如果超过了，说明已经过期了，就会使用协商缓存（如果浏览器不支持http1.1，就会使用expires进行过期的判断）
- 使用协商缓存，浏览器先会向服务器发送带有if-None-Match和if-Modified-Since的请求，服务器收到请求之后，首先会判断Etag值是否一致，如果一致，说明资源文件没有被修改，就会命中协商缓存，返回304；如果不一致，说明资源文件修改了，就会返回200，并且返回新的资源文件和新的Etag值。
- 如果请求中没有Etag，那么浏览器就会比较if-Modified-Since和Last-Modified，如果一致说明资源未改变，命中协商缓存，返回304；如果不一致，说明资源改变，返回200，并且返回新的资源文件和新的last-modified

### 5.为什么需要浏览器缓存？

### 6.用户点击刷新按钮或者按 F5、按 Ctrl+F5 （强制刷新）、地址栏回车有什么区别？

### 7.浏览器内核

- Chrome ：Blink
- FireFox：Gecko
- IE：trident
- Safari：Webkit
- Opera：Presto -> Webkit -> Blink

### 8.浏览器的渲染过程

### 9.浏览器渲染优化

### 10.渲染过程中遇到 JS 文件如何处理？

### 11.Cookie、LocalStorage、SessionStorage区别

- Cookie会携带在http请求中，即会在客户端和服务端之间来回传递，而LocalStorage和SessionStorge只会保存在本地，另外Cookie的很小，大约只有4K，LocalStorge大小一般为5MB，可以存储更多的信息。
- SessionStorage只在浏览器窗口关闭之前有效，即当浏览器窗口关闭之后，SessionStorage就被清除了；LocalStorage会永久保存在本地，而Cookie有一个失效时间，在失效时间内，Cookie才是有效的。
- Cookie和localStorage在所有同源窗口中都是共享的

### 12.Cookie 和 Session 区别

- Cookie存放在浏览器中，而Session存放在服务器中
- Cookie不是很安全，别人可以分析存放在本地的Cookie进行欺骗，考虑到安全性应该使用Session
- Session保存在服务器上，如果访问增多，会比较占用服务器的性能
- 单个Cookie保存的数据不能超过4K，很多浏览器都限制了一个站点最多保存20个Cookie

### 13.什么是同源策略

- 指的是协议号、域名、端口号必须一致
- 同源策略是为了保证用户的信息安全，它只是一种对Js脚本的限制，而不是对浏览器的限制，所以对于一般的img或者script不会有跨域的限制

### 14.如何解决跨越问题

1. JSONP
   - 原理是利用script标签没有跨域限制，通过script标签的src属性，发送带有callback参数的GET请求
2. CORS
3. postMessage跨域
4. nginx代理跨域

---

## 性能优化

### 1.CDN

### 2.懒加载与预加载的区别

### 3.回流与重绘

回流：

当渲染树中的部分或全部元素的尺寸、结构或属性发生变化时，浏览器会重新渲染部分或全部元素，这个过程叫做回流。触发回流，会导致周围的其它元素重新排列。

重绘：

页面中的某些元素的样式发生改变，但不会影响到它在文档流中的位置，浏览器就会对它进行重新绘制，这一个过程就叫做重绘。比如修改元素的背景色或者前景色。

回流一定会导致重绘，而重绘不一定引发回流。

减少回流和重绘：

1. 使用absoluted和fixed定位，让元素脱离文档流，这样就不会影响到文档流中的其它元素了。
2. 避免频繁操作DOM。可以创建一个文档片段documentFragment，将所有DOM操作都放到文档片段中，然后再把它假如到文档中。
3. 不要频繁操作元素的样式。
4. 将元素设置为display：none，当操作结束后，再把它显示出来，因为display为none的元素上进行DOM操作不会引发回流和重绘

### 4.前端优化

- 降低请求量
  - 合并资源
  - 减少HTTP请求数
  - minify/gzip压缩
  - webP
  - lazyLoad
- 提高访问速度
  - 预解析DNS
  - 减少域名数
  - 并行加载
  - CDN分发
- 使用缓存
  - HTTP缓存请求
  - 离线缓存manifest
  - localStorage
- 渲染
  - JS/CSS优化
  - 加载顺序
  - 服务端渲染
  - pipeline

## 手写代码

### 1.map

```js
Array.prototype._map = function(fn) {
  if (typeof fn !== 'function') {
    throw Error('参数必须是函数')
  }
  const rst = []
  for (let i = 0, len = this.length; i < len; i++) {
    rst.push(fn(this[i]))
  }
  return rst
}
const arr = [1, 2, 3]
const rst = arr._map(item => item * 2)
console.log(rst);
```

### 2.filter

```js
Array.prototype._filter = function(fn) {
  if (typeof fn !== 'function') {
    throw new Error('参数必须是函数')
  }
  const rst = []
  for (let i = 0, len = this.length; i < len; i++) {
    fn(this[i]) && rst.push(this[i])
  }
  return rst
}
const arr = [1, 2, 3, 4]
const rst = arr._filter(item => item % 2 === 0)
console.log(rst);
```

### 3.reduce

```js
Array.prototype._reduce = function(fn, initVal) {
  if (typeof fn !== 'function') {
    throw Error('第一个参数必须是函数')
  }
  let value, i
  if (initVal === undefined) {
    value = this[0]
    i = 1
  } else {
    value = initVal
    i = 0
  }
  for (i, len = this.length; i < len; i++) {
    value = fn(value, this[i], i, this)
  }
  return value
}
const arr = [1, 2, 3, 4]
const rst = arr._reduce((p, c, i, a) => {
  console.log(p, c, i, a);
  return p + c
}, 20)
console.log(rst);
```

### 4.浅拷贝

`如果拷贝的是基本数据类型，拷贝的就是基本数据类型的值；如果是引用数据类型，拷贝的就是内存地址。如果其中一个对象的引用内存地址发生改变，另一个对象也会发生变化。`

实现方式：

```js
// --------------------------1.Object.assign-----------------------------------
const obj1 = {sports: ['basketball', 'football', 'swim']}
const obj2 = {info: {name: 'obj2', gender: 'male', age: 10}}
// 第一个参数为{}，返回一个新对象
const newObj = Object.assign({}, obj1, obj2)
// 第一个参数不为{}，返回第一个参数
// Object.assign(obj1, obj2)

// 浅拷贝，地址共用
console.log(newObj);
obj1.sports[0] = 'basket'
obj2.info.age = 25
console.log(newObj);
newObj.sports[0] = '111'
newObj.info.name = '222'
console.log(obj1);
console.log(obj2);

// --------------------------2.扩展运算符-----------------------------------------
const obj1 = {
  sports: ['basket', 'football'],
  info: {
    name: 'obj1',
    gender: 'male'
  }
}
const newObj = {...obj1}
console.log(newObj);
// 浅拷贝，地址共用
obj1.sports[0] = 'basketball'
obj1.info.name = 'obj1111'
console.log(newObj);

// --------------------------3.Array.prototype.slice-----------------------------------------
const arr = [
  {
    name: 'arr',
    age: 18
  },
  ['basket', 'football']
]
const newArr = arr.slice()
console.log(newArr);
// 浅拷贝，地址共用
arr[0].name = 'arr1111'
arr[1][0] = 'basketball'
console.log(newArr);

// --------------------------4.Array.prototype.concat-----------------------------------------
const arr = [
  {
    name: 'arr',
    age: 18
  },
  ['basket', 'football']
]
const newArr = arr.concat()
console.log(newArr);
// 浅拷贝，地址共用
arr[0].name = 'arr1111'
arr[1][0] = 'basketball'
console.log(newArr);
```

手写：

```js
function shallowCopy(obj) {
  if (!obj || typeof obj !== 'object') return
  const newObj = Array.isArray(obj) ? [] : {}
  for (let key in obj) {
    // hasOwnProperty用于判断对象属性是否是实例上的属性，原型对象上的属性不算
    if (obj.hasOwnProperty(key)) {
      newObj[key] = obj[key] // 本质上，赋值的是内存地址
    }
  }
  return newObj
}
```

### 5.深拷贝

实现方式：

```js
// JSON.stringify()
const obj = {
  info: {
    name: 'obj'
  }
}
const newObj = JSON.parse(JSON.stringify(obj))
console.log(newObj); // { info: { name: 'obj' } }
obj.info.name = 'obj111'
console.log(obj); // { info: { name: 'obj111' } }
console.log(newObj); // { info: { name: 'obj' } }

// 缺陷：拷贝的对象中如果有函数，undefined，symbol，当使用过JSON.stringify()进行处理之后，都会消失。
// 比如：
const obj = {
  info: Symbol(),
  gender: undefined,
  getName() {
    console.log('getName');
  }
}
const newObj = JSON.parse(JSON.stringify(obj))
console.log(newObj); // {}
```

手写：

```js
function deepCopy(obj) {
  if (!obj || typeof obj !== 'object') return
  const newObj = Array.isArray(obj) ? [] : {}
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      // 递归实现引用类型的拷贝
      newObj[key] = typeof obj[key] === 'object' ? deepCopy(obj[key]) : obj[key]
    }
  }
  return newObj
}
```

### 6.call

`fn.call(thisArg, param1, param2, ...)`

```js
Function.prototype._call = function(context, ...args) {
  if (typeof this !== 'function') {
    throw new Error('this must be a function')
  }
  context = context || window // 获取上下文对象
  context.fn = this // 使用context的fn调用该方法，从而改变this指向
  let rst = context.fn(...args) // 获取结果
  delete context.fn // 删除属性
  return rst // 返回结果
}

//---------------------- 测试 -----------------------------------------
const obj1 = {
  name: 'obj1',
  getName(greet) {
    console.log(`${greet}_${this.name}!`);
  }
}
const obj2 = {
  name: 'obj2'
}
obj1.getName._call(obj2, 'hello') // hello_obj2!
```

### 7.apply

`fn.apply(thisArg, [param1,param2,...])`

```js
Function.prototype._apply = function(context, args) {
  if (typeof this !== 'function') {
    throw new Error('this must be a function')
  }
  context = context || window
  context.fn = this
  let rst = args ? context.fn(...args) : context.fn()
  delete context.fn
  return rst
}

//---------------------- 测试 -----------------------------------------
const obj1 = {
  name: 'obj1',
  getName(greet) {
    console.log(`${greet}_${this.name}!`);
  }
}
const obj2 = {
  name: 'obj2'
}
obj1.getName._apply(obj2, ['hello']) // hello_obj2!
```

### 8.bind

`fn.bind(thisArg, param1, param2, ...)`

```js
Function.prototype._bind = function(context, ...args) {
  if (typeof this !== 'function') {
    throw new Error('this must be a function')
  }
  const self = this
  const fn = function() {
    return self.apply(
      this instanceof fn ? this : context, // 返回函数如果作为构造函数
      args.concat(...arguments) // 拼接_bind传入的参数
    )
  }
  if (this.prototype) { // 如果函数有原型，那么返回的绑定函数也要有相同的原型
    fn.prototype = Object.create(this.prototype)
  }
  return fn
}

//---------------------- 测试 -----------------------------------------
const obj1 = {
  name: 'obj1',
  getName(...args) {
    console.log(`${args}_${this.name}!`);
  }
}
const obj2 = {
  name: 'obj2'
}
const a = obj1.getName._bind(obj2, 'hi')
a('hello') // hi,hello_obj2!
```

### 9.函数柯里化

函数柯里化主要有3个作用： **参数复用**、**提前返回**和 **延迟执行**

```js
function curry(fn, args) {
  // 获取函数需要的参数长度
  let length = fn.length;

  args = args || [];

  return function() {
    let subArgs = args.slice(0);

    // 拼接得到现有的所有参数
    for (let i = 0; i < arguments.length; i++) {
      subArgs.push(arguments[i]);
    }

    // 判断参数的长度是否已经满足函数所需参数的长度
    if (subArgs.length >= length) {
      // 如果满足，执行函数
      return fn.apply(this, subArgs);
    } else {
      // 如果不满足，递归返回科里化的函数，等待参数的传入
      return curry.call(this, fn, subArgs);
    }
  };
}

// es6 实现
function curry(fn, ...args) {
  return fn.length <= args.length ? fn(...args) : curry.bind(null, fn, ...args);
}
```

### 10.Ajax请求

普通：

```js
const url = './index.html'
const xhr = window.XmlHttpRequest ? new XmlHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP')
xhr.open('GET', url, true)
xhr.onreadystatechange = function() {
  if (this.readyState !== 4) return
  if (this.status === 200) {
    handle(this.response)
  } else {
    console.error(this.statusText)
  }
}
xhr.onerror = function() {
  console.error(this.statusText);
}
xhr.responseType = 'json'
xhr.setRequestHeader('Accept', 'application/json')
xhr.send(null)
```

用 Promise 封装：

```js
function ajax(url) {
  return new Promise((resolve, reject) => {
    const xhr = window.XmlHttpRequest ? new XmlHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP')
    xhr.open('GET', url, true)
    xhr.onreadystatechange = function() {
      if (this.readyState !== 4) return
      if (this.status === 200 || this.status === 304) {
        resolve(this.response)
      } else {
        reject(new Error(this.statusText))
      }
    }
    xhr.onerror = function() {
      reject(new Error(this.statusText))
    }
    xhr.responseType = 'json'
    xhr.setRequestHeader('Accept', 'application/json')
    xhr.send(null)
  })
}
```

### 11.new

```js
function _new(constructor, ...args) {
  if (typeof constructor !== 'function') {
    throw new Error('must be a function')
  }
  // 重新开辟一块内存空间，复制了对象的原型
  const newObj = Object.create(constructor.prototype)
  // 用newObj调用构造函数，将构造函数里的属性或方法添加进去
  const rst = constructor.call(newObj, ...args)
  // 如果构造函数返回的是对象、数组(包括在object中)或者函数，就直接返回这个结果
  if (rst && (typeof rst === 'object' || typeof rst === 'function')) {
    return rst
  }
  // 否则返回这个新创建的对象
  return newObj
}

//---------------------- 测试 -----------------------------------------
function Demo(name, age) {
  this.name = name
  this.age = age
  // return {} // 如果有返回值且为引用类型的话，生成的实例就为这个值，否则为实例的地址
}
Demo.prototype.getName = function() {
  console.log(this.name);
}
const d = _new(Demo, 'jack', 18)
console.log(d); // Demo { name: 'jack', age: 18 }
```

### 12.promise

```js
const PENDING = 'pending'
const RESOLVED = 'resolved'
const REJECTED = 'rejected'

function _Promise(fn) {
  const self = this
  this.state = PENDING
  this.value = null
  this.resolvedCallbacks = []
  this.rejectedCallbacks = []

  // 声明resolve函数
  function resolve(value) {
    // 如果传入resolve的参数是一个Promise实例
    if (value instanceof _Promise) {
      return value.then(resolve, reject)
    }
    // 宏任务，放在同步代码之后执行
    setTimeout(() => {
      // 只有为等待状态时，才能更变状态并修改值
      if (self.state === PENDING) {
        self.state = RESOLVED
        self.value = value
        self.resolvedCallbacks.forEach(callback => {
          callback(value)
        })
      }
    }, 0)
  }

  function reject(value) {
    setTimeout(() => {
      if (self.state === PENDING) {
        self.state = REJECTED
        self.value = value
        self.rejectedCallbacks.forEach(callback => {
          callback(value)
        })
      }
    }, 0);
  }

  try {
    fn(resolve, reject)
  } catch (ex) {
    reject(ex)
  }
}

_Promise.prototype.then = function(onResolved, onRejected) {
  const self = this
  // 链式调用
  return new _Promise((resolve, reject) => {
    const resolved = () => {
      try {
        const rst = onResolved(self.value)
        return rst instanceof _Promise ? rst.then(resolve, reject) : resolve(rst)
      } catch (ex) {
        reject(ex)
      }
    }
    const rejected = () => {
      try {
        const rst = onRejected(self.value)
        return rst instanceof _Promise ? rst.then(resolve, reject) : reject(rst)
      } catch (ex) {
        reject(ex)
      }
    }

    switch (self.state) {
      case PENDING:
        self.resolvedCallbacks.push(resolved)
        self.rejectedCallbacks.push(rejected)
        break
      case RESOLVED:
        resolved()
        break
      case REJECTED:
        rejected()
        break
    }
  })
}

//---------------------- 测试 -----------------------------------------
const p = new _Promise((resolve, reject) => {
  var a = 1
  if (a === 11) {
    resolve(a)
  } else {
    reject('error!!!')
  }
})
p.then(res => {
  console.log(res);
}, err => {
  console.log(err);
})
```

### 13.instanceof

```js
function _instanceof(left, right) {
  let proto = Object.getPrototypeOf(left),
      prototype = right.prototype
  while (true) {
    if (!proto) return false
    if (proto === prototype) return true
    proto = Object.getPrototypeOf(proto)
  }
}
```

### 14.防抖、节流

**函数防抖** 是指在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。这可以使用在一些点击请求的事件上，避免因为用户的多次点击向后端发送多次请求。

**函数节流** 是指规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。节流可以使用在 scroll 函数的事件监听上，通过事件节流来降低事件调用的频率。

```js
function debounce(fn, wait) {
  let timer = null
  return function() {
    let self = this,
        args = arguments
    if (timer) {
      clearTimeout(timer)
      timer = null
    }
    timer = setTimeout(() => {
      return fn.call(self, ...args)
    }, wait)
  }
}

function throttle(fn, delay) {
    let prev = Date.now()
    return function() {
        let self = this,
            args = arguments,
            cur = Date.now()
       	if (cur - prev >= delay) {
            prev = Date.now()
            return fn.call(self, ...args)
        }
    }
}
```

