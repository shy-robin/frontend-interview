# JS EventLoop

## 进程与线程

### 进程

- 进程是 `CPU` 资源分配的最小单位
- 电脑打开一个软件就会创建一个或多个进程，`CPU` 为每个进程分配资源空间
- 每个进程之间相互独立，数据不共享

### 线程

- 线程是 `CPU` 调度的最小单位
- 一个进程可以有多个线程

### 进程和线程的区别

- 进程之间相互独立，但是同一进程的各个线程之间共享程序的内存空间（包括代码段、数据集、堆等）和一些进程级的资源（如打开文件和信号）
- 调度和切换：线程上下文切换比进程上下文切换要快得多

### 多进程和多线程

- 多进程：计算机中有两个及两个以上的进行处于运行状态。带来的好处是：比如可以在浏览网页的时候听歌，两个进程之间互不干扰
- 多线程：一个程序中可以创建多个不同的线程并行地执行不同的任务，提高执行效率

### 单线程的JS

JS的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？

还有人说js还有Worker线程，对的，为了利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程，但是子线程是完全受主线程控制的，而且不得操作DOM。所以，这个标准并没有改变JavaScript是单线程的本质。

## 同步与异步

### 同步

如果在函数返回的时候，调用者就能够得到预期结果(即拿到了预期的返回值或者看到了预期的效果)，那么这个函数就是同步的。

**如果函数是同步的，即使调用函数执行的任务比较耗时，也会一直等待直到得到预期结果。**

### 异步

如果在函数返回的时候，调用者还不能够得到预期结果，而是需要在将来通过一定的手段得到，那么这个函数就是异步的。

**如果函数是异步的，发出调用之后，马上返回，但是不会马上返回预期结果。调用者不必主动等待，当被调用者得到结果之后会通过回调函数主动通知调用者。**

### 异步过程的构成要素

一个异步过程通常是这样的：

> 主线程发起一个异步请求，相应的工作线程接收请求并告知主线程已收到(异步函数返回)；主线程可以继续执行后面的代码，同时工作线程执行异步任务；工作线程完成工作后，通知主线程；主线程收到通知后，执行一定的动作(调用回调函数)。

`异步函数`通常具有以下的形式：

```
A(args..., callbackFn)
```

它可以叫做异步过程的发起函数，或者叫做异步任务注册函数。`args`是这个函数需要的参数。`callbackFn`也是这个函数的参数，但是它比较特殊所以单独列出来。

`异步函数`实际上很快就调用完成了。但是后面还有工作线程执行异步任务、通知主线程、主线程调用回调函数等很多步骤。我们把整个过程叫做`异步过程`。异步函数的调用在整个异步过程中，只是一小部分。

所以，从主线程的角度看，一个异步过程包括下面两个要素：

- 发起函数(或叫注册函数)`A`
- 回调函数`callbackFn`

它们都是在主线程上调用的，其中注册函数用来发起异步过程，回调函数用来处理结果。

举个具体的例子：

```
setTimeout(fn, 1000);
```

其中的`setTimeout`就是异步过程的发起函数，`fn`是回调函数。

注意：前面说的形式`A(args..., callbackFn)`只是一种抽象的表示，并不代表回调函数一定要作为发起函数的参数，例如：

```
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = xxx; // 添加回调函数
xhr.open('GET', url);
xhr.send(); // 发起函数
```

发起函数和回调函数就是分离的。

---

既然JavaScript是单线程，怎么还存在异步，那些耗时操作到底交给谁去执行了？

JavaScript其实就是一门语言，说是单线程还是多线程得结合具体运行环境。JS的运行通常是在浏览器中进行的，具体由JS引擎去解析和运行。下面我们来具体了解一下浏览器。

## 浏览器

### 浏览器进程

#### Browser进程

- 浏览器的主进程(负责协调、主控)，该进程只有一个
- 负责浏览器界面显示，与用户交互。如前进，后退等
- 负责各个页面的管理，创建和销毁其他进程
- 将渲染(Renderer)进程得到的内存中的Bitmap(位图)，绘制到用户界面上
- 网络资源的管理，下载等

#### 第三方插件进程

- 每种类型的插件对应一个进程，当使用该插件时才创建

#### GPU进程

- 该进程也只有一个，用于3D绘制等等

#### 渲染进程(重点)

- 即通常所说的浏览器内核(Renderer进程，内部是多线程)
- 每个Tab页面都有一个渲染进程，互不影响
- 主要作用为页面渲染，脚本执行，事件处理等

### 渲染进程的五大线程

页面的渲染，JS的执行，事件的循环，都在渲染进程内执行，所以要重点了解渲染进程。

渲染进程是多线程的，我们来看渲染进程的一些常用较为主要的线程。

#### 1.JS引擎线程

JS引擎线程就是JS内核，负责处理Javascript脚本程序(例如V8引擎)

JS引擎线程负责解析Javascript脚本，运行代码

JS引擎一直等待着任务队列中任务的到来，然后加以处理

- 浏览器同时只能有一个JS引擎线程在运行JS程序，所以js是单线程运行的
- 一个Tab页(renderer进程)中无论什么时候都只有一个JS线程在运行JS程序

**GUI渲染线程与JS引擎线程是互斥的，js引擎线程会阻塞GUI渲染线程**

- 就是我们常遇到的JS执行时间过长，造成页面的渲染不连贯，导致页面渲染加载阻塞(就是加载慢)
- 例如浏览器渲染的时候遇到`<script>`标签，就会停止GUI的渲染，然后js引擎线程开始工作，执行里面的js代码，等js执行完毕，js引擎线程停止工作，GUI继续渲染下面的内容。所以如果js执行时间太长就会造成页面卡顿的情况

#### 2.GUI渲染线程

- 负责渲染浏览器界面，解析HTML，CSS，构建DOM树和RenderObject树，布局和绘制等
  - 解析html代码(HTML代码本质是字符串)转化为浏览器认识的节点，生成DOM树，也就是DOM Tree
  - 解析css，生成CSSOM(CSS规则树)
  - 把DOM Tree 和CSSOM结合，生成Rendering Tree(渲染树)
- 当我们修改了一些元素的颜色或者背景色，页面就会重绘(Repaint)
- 当我们修改元素的尺寸，页面就会回流(Reflow)
- 当页面需要Repainting和Reflow时GUI线程执行，绘制页面
- 回流(Reflow)比重绘(Repaint)的成本要高，我们要尽量避免Reflow和Repaint
- GUI渲染线程与JS引擎线程是互斥的
  - 当JS引擎执行时GUI线程会被挂起(相当于被冻结了)
  - GUI更新会被保存在一个队列中等到JS引擎空闲时立即被执行

#### 3.事件触发线程

- 属于浏览器而不是JS引擎，用来控制事件循环，并且管理着一个事件队列(task queue)
- 当js执行碰到事件绑定和一些异步操作(如setTimeOut，也可来自浏览器内核的其他线程，如鼠标点击、AJAX异步请求等)，会走事件触发线程将对应的事件添加到对应的线程中(比如定时器操作，便把定时器事件添加到定时器线程)，等异步事件有了结果，便把他们的回调操作添加到事件队列，等待js引擎线程空闲时来处理。
- 当对应的事件符合触发条件被触发时，该线程会把事件添加到待处理队列的队尾，等待JS引擎的处理
- 因为JS是单线程，所以这些待处理队列中的事件都得排队等待JS引擎处理

#### 4.定时触发器线程

- `setInterval`与`setTimeout`所在线程
- 浏览器定时计数器并不是由JavaScript引擎计数的(因为JavaScript引擎是单线程的，如果处于阻塞线程状态就会影响记计时的准确)
- 通过单独线程来计时并触发定时(计时完毕后，添加到事件触发线程的事件队列中，等待JS引擎空闲后执行)，这个线程就是定时触发器线程，也叫定时器线程
- W3C在HTML标准中规定，规定要求`setTimeout`中低于4ms的时间间隔算为4ms

#### 5.异步http请求线程

- 在XMLHttpRequest在连接后是通过浏览器新开一个线程请求
- 将检测到状态变更时，如果设置有回调函数，异步线程就产生状态变更事件，将这个回调再放入事件队列中再由JavaScript引擎执行
- 简单说就是当执行到一个http异步请求时，就把异步请求事件添加到异步请求线程，等收到响应(准确来说应该是http状态变化)，再把回调函数添加到事件队列，等待js引擎线程来执行

## 事件循环

异步过程中，工作线程在异步操作完成后需要通知主线程。那么这个**通知机制**是怎样实现的呢？答案是利用消息队列和事件循环。

用一句话概括：工作线程将消息放到消息队列，主线程通过事件循环过程去取消息。

- **消息队列**：消息队列是一个先进先出的队列，它里面存放着各种消息。
- **事件循环**：事件循环是指主线程重复从消息队列中取消息、执行的过程。

实际上，主线程只会做一件事情，就是从消息队列里面取消息、执行消息，再取消息、再执行。当消息队列为空时，就会等待直到消息队列变成非空。而且主线程只有在将当前的消息执行完成后，才会去取下一个消息。这种机制就叫做事件循环机制，取一个消息并执行的过程叫做一次循环。

那么，消息队列中放的**消息**具体是什么东西？消息的具体结构当然跟具体的实现有关，但是为了简单起见，我们可以认为：

> 消息就是注册异步任务时添加的回调函数。

再次以异步AJAX为例，假设存在如下的代码：

```
$.ajax('http://segmentfault.com', function(resp) {
    console.log('我是响应：', resp);
});

// 其他代码
...
...
...
```

主线程在发起AJAX请求后，会继续执行其他代码。AJAX线程负责请求`segmentfault.com`，拿到响应后，它会把响应封装成一个JavaScript对象，然后构造一条消息：

```
// 消息队列中的消息就长这个样子
var message = function () {
    callbackFn(response);
}
```

其中的`callbackFn`就是前面代码中得到成功响应时的回调函数。

主线程在执行完当前循环中的所有代码后，就会到消息队列取出这条消息(也就是`message`函数)，并执行它。到此为止，就完成了工作线程对主线程的`通知`，回调函数也就得到了执行。如果一开始主线程就没有提供回调函数，AJAX线程在收到HTTP响应后，也就没必要通知主线程，从而也没必要往消息队列放消息。

用图表示这个过程就是：

![](https://gitee.com/gainmore/imglib/raw/master/img/20210707133407.png)

## 宏任务和微任务

### 宏任务(macrotask)

在`ECMAScript`中，`macrotask`也被称为`task`

我们可以将每次执行栈执行的代码当做是一个宏任务(包括每次从事件队列中获取一个事件回调并放到执行栈中执行)， 每一个宏任务会从头到尾执行完毕，不会执行其他

由于`JS引擎线程`和`GUI渲染线程`是互斥的关系，浏览器为了能够使`宏任务`和`DOM任务`有序的进行，会在一个`宏任务`执行结果后，在下一个`宏任务`执行前，`GUI渲染线程`开始工作，对页面进行渲染

```
宏任务 -> GUI渲染 -> 宏任务 -> ...
```

常见的宏任务

- 主代码块(script)
- `setTimeout`
- `setInterval`
- `setImmediate -> Node`
- `requestAnimationFrame -> 浏览器`

### 微任务(microtask)

`ES6`新引入了Promise标准，同时浏览器实现上多了一个`microtask`微任务概念，在`ECMAScript`中，`microtask`也被称为`jobs`

我们已经知道`宏任务`结束后，会执行渲染，然后执行下一个`宏任务`， 而微任务可以理解成在当前`宏任务`执行后立即执行的任务

当一个`宏任务`执行完，会在渲染前，将执行期间所产生的所有`微任务`都执行完

```
宏任务 -> 微任务 -> GUI渲染 -> 宏任务 -> ...
```

常见微任务

- `process.nextTick -> Node`
- `Promise.then()`
- `Promise.catch()`
- `Promise.finally()`
- `Object.observe (已废弃)`
- `MutationObserver`

### 宏任务和微任务区分

浏览器会先执行一个宏任务，紧接着执行当前执行栈产生的微任务，再进行渲染，然后再执行下一个宏任务

**微任务和宏任务不在一个任务队列**

- 例如`setTimeout`是一个宏任务，它的事件回调在宏任务队列，`Promise.then()`是一个微任务，它的事件回调在微任务队列，二者并不是一个任务队列
- 以Chrome 为例，有关渲染的都是在渲染进程中执行，渲染进程中的任务（DOM树构建，js解析…等等）需要主线程执行的任务都会在主线程中执行，而浏览器维护了一套事件循环机制，主线程上的任务都会放到消息队列中执行，主线程会循环消息队列，并从头部取出任务进行执行，如果执行过程中产生其他任务需要主线程执行的，渲染进程中的其他线程会把该任务塞入到消息队列的尾部，消息队列中的任务都是宏任务
- 微任务是如何产生的呢？当执行到script脚本的时候，js引擎会为全局创建一个执行上下文，在该执行上下文中维护了一个微任务队列，当遇到微任务，就会把微任务回调放在微队列中，当所有的js代码执行完毕，在退出全局上下文之前引擎会去检查该队列，有回调就执行，没有就退出执行上下文，这也就是为什么微任务要早于宏任务，也是大家常说的，每个宏任务都有一个微任务队列（由于定时器是浏览器的API，所以定时器是宏任务，在js中遇到定时器会也是放入到浏览器的队列中）

## 图解

![](https://gitee.com/gainmore/imglib/raw/master/img/EventLoop2.png)

这里有一个 `index.html` 文件，我们可以将它运行在浏览器上，然后分析它运行的整个过程。

```html
<html>
  <head>...</head>
  <body>...</body>
  <script>
    var a = 'hello world'
    console.log(a);
    new Promise(function(resolve, reject) {
      console.log('promise1');
      resolve('hi1')
    }).then(function(res) {
      console.log(res);
    })

    function first() {
      console.log('Inside first function');
      second()
      setTimeout(function() {
        console.log('timer2');
        new Promise(function(resolve, reject) {
          console.log('promise3');
          resolve('hi3')
        }).then(function(res) {
          console.log(res);
        })
      }, 1000)
    }

    function second() {
      console.log('Inside second function');
      document.body.style = 'background:black';
      document.body.style = 'background:red';
      document.body.style = 'background:blue';
      document.body.style = 'background:pink';
    }

    first()

    setTimeout(function() {
      console.log('timer1');
      new Promise(function(resolve, reject) {
        console.log('promise4');
        resolve('hi4')
      }).then(function(res) {
        console.log(res);
      })
    }, 0)

    new Promise(function(resolve, reject) {
      console.log('promise2');
      resolve('hi2')
    }).then(function(res) {
      console.log(res);
    })  
  </script>
</html>
```

1. `GUI渲染线程` 解析 `HTML`，遇到 `script` 停止解析，交给 `JS引擎线程` 处理 `JS`，`GUI渲染线程`停止工作；
2. `JS引擎线程` 处理 `script` 这个宏任务： 创建全局执行上下文(`Global Execution Contenxt`)并将其压入到 `执行栈` 中，开始从上到下逐行解析 `JS`；
3. `JS引擎线程` 只处理同步代码，首先创建变量 `a`，然后打印 `a`；然后执行异步函数 `Promise` 并执行里面的同步代码（打印 `promise1`，然后 resolve），完成之后，返回异步函数执行结果（一个promise对象），同时将 `.then()` 放入到`微任务队列` 中；
4. 之后，将 `first` 函数执行上下文(`Function Execution Context`) 压入到执行栈中，然后从上到下执行函数 `first` 的代码；
5. 首先，打印 `Inside first function`，然后将 `second函数执行上下文`压入到执行栈中，然后执行 `second` 中的代码；
6. 在 `second` 中，打印 `Inside second function`，然后执行后面四条代码，属于同一次宏任务，全部执行完后将这四条 `GUI更新` 添加到 `GUI更新队列` 中；
7. `second` 函数执行完毕，将 `second函数执行上下文` 弹出执行栈；
8. 继续执行 `first函数执行上下文`，执行了 `setTimeout` 这个异步函数，主线程（`JS引擎线程`）很快获取到异步函数的返回结果并向 `定时触发器线程` 发送通知，`定时触发器线程` 收到通知后，会在 `1 s` 后向由 `事件触发线程` 管理的 `宏任务队列` 中添加回调函数；
9. `first 函数` 执行完毕，将其上下文弹出执行栈，然后继续执行全局上下文中的代码；
10. 执行 `setTimeout` 这个异步函数，主线程获取到异步函数的返回结果并向 `定时触发器线程` 发送通知，`定时触发器线程`收到通知后，会在 `0 s` 后向由 `事件触发线程` 管理的 `宏任务队列` 中添加回调函数；
11. 执行 `Promise` 这个异步函数，里面的同步函数立即执行（打印 `promise2`并 `resolve`），主线程获取到异步函数的返回结果（一个 promise 对象），同时将 `.then()` 放入到`微任务队列` 中；
12. `script` 宏任务执行完毕，主线程检查 `微任务队列` 是否有微任务：有两个 `.then()`，执行队列中第一个任务的回调函数：打印 `hi1`。执行完毕后弹出该任务，继续执行队列中第一个任务的回调函数：打印 `hi2`。执行完毕后弹出该任务；
13. 微任务队列为空，主线程检查 `GUI更新队列` 是否有内容：有四条 `GUI更新`，所以主线程停止工作，交由 `GUI渲染线程` 处理 `GUI更新` ，渲染时`GUI渲染线程`会将所有UI改动优化合并，所以视觉上，只会看到页面背景色变成 `pink`；
14. `GUI渲染` 处理完毕，`GUI渲染线程` 停止工作，主线程开始工作，进入下一轮事件循环；
15. 主线程检查 `宏任务队列` 中是否有宏任务：有两个 `setTimeout`，执行队列中第一个任务的回调函数：打印 `timer1`，执行异步函数 `Promise`里面的同步代码：打印 `promise4以及resolve`，主线程获取到异步函数返回结果，并将 `.then()` 添加到微任务队列中；
16. 第一个宏任务执行完毕，检查 `微任务队列` 是否有微任务：有一个 `.then()`，执行 `.then()`，打印 `hi4`；
17. 微任务队列执行完毕，检查是否有 `GUI更新`：没有。进行下一个事件循环；
18. 执行宏任务：打印 `timer2`，执行异步函数 `Promise` 里的同步代码：`打印 promise3以及resolve`，主线程获取异步函数返回结果（一个promise对象），然后向微任务队列添加 `.then()`；
19. 宏任务执行完毕，检查微任务队列是否有任务：一个`.then()`，执行该任务：打印 `hi3`；
20. 微任务队列执行完毕，检查 `GUI更新队列`：无GUI更新；
21. 无宏任务，执行完毕；
22. 全局执行上下文从执行栈中弹出，`script` 执行完毕。

## 总结

`JS` 中的异步任务可以分为 `宏任务` 和 `微任务`，`微任务` 主要是 `Promise` 产生的一些处理函数，因为 `Promise` 是内置在 `JS 引擎` 中的，所以不需要交给其他线程处理，是被 `JS引擎线程` 直接添加到 `微任务队列` 中。这是 `微任务` 和 `宏任务` 之间差异之一。

## 参考文章

1. [「硬核JS」一次搞懂JS运行机制](https://juejin.cn/post/6844904050543034376#heading-27)
2. [JS线程、Event Loop、事件循环、任务队列、宏任务](https://juejin.cn/post/6844903752621637645#comment)
3. [微任务、宏任务与Event-Loop](https://juejin.cn/post/6844903657264136200#heading-3)
4. [JavaScript异步机制详解](https://juejin.cn/post/6844903556084924423#heading-0)
5. [JavaScript：彻底理解同步、异步和事件循环(Event Loop)](https://segmentfault.com/a/1190000004322358)
6. [[译] 理解 JavaScript 中的执行上下文和执行栈](https://juejin.cn/post/6844903682283143181#heading-0)
7. [JavaScript执行上下文-执行栈](https://juejin.cn/post/6844904199063339015#comment)

