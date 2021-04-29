### Shadow DOM

https://juejin.cn/post/6844903841033355271

封装一个DOM放到一个 host element里

### Tree Shaking
链接：https://www.nowcoder.com/questionTerminal/2d5bb94ca6cf4b8cb61f4f7e424b51e2
来源：牛客网

Tree Shaking用于移除 JavaScript 上下文中的未引用代码(dead-code)。
Code Splitting可以将代码分成多个捆绑包，然后可以按需或并行加载。
模块热替换(HMR - hot module replacement)会在应用程序运行过程中，替换、添加或删除模块，而无需重新加载整个页面。
Source Mapping是从已转换的代码映射到原始源的文件，使浏览器能够重构原始源并在调试器中显示重建的原始源

### 浏览器缓存与js运行机制

https://www.jianshu.com/p/5c23bdcf2a11

Javascript 是单线程
通过任务队列实现

所谓”回调函数”（callback），就是那些会被主线程挂起来的代码。异步任务必须指定回调函数，当主线程开始执行异步任务，就是执行对应的回调函数。
为了利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程，但是子线程完
全受主线程控制，且不得操作DOM。所以，这个新标准并没有改变JavaScript单线程的本质。

（1）所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
（4）主线程不断重复上面的第三步。

作者：Zulu_c02a
链接：https://www.jianshu.com/p/5c23bdcf2a11
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

作者：云澹
链接：https://www.zhihu.com/question/31982417/answer/54136684
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

补充：JS中其实是没有线程概念的，所谓的单线程也只是相对于多线程而言。JS的设计初衷就没有考虑这些，针对JS这种不具备并行任务处理的特性，我们称之为“单线程”。
***************华丽的分割线*******************************一段代码就能证明了啊。
```
function foo() {
    console.log("first");
    setTimeout(( function(){
        console.log( 'second' );
    }),5);
}
 
for (var i = 0; i < 1000000; i++) {
    foo();
}
```
执行结果会首先全部输出first，然后全部输出second；尽管中间的执行会超过5ms。Javascript是单线程的JS运行在浏览器中，是单线程的，每个window一个JS线程，既然是单线程的，在某个特定的时刻只有特定的代码能够被执行，并阻塞其它的代码。而浏览器是事件驱动的（Event driven），浏览器中很多行为是异步（Asynchronized）的，会创建事件并放入执行队列中。javascript引擎是单线程处理它的任务队列。所以当多个事件触发时，会依次放入队列，然后一个一个响应。（所以上面的代码是5ms后把输出second的任务加入队列，而当前有任务，所以只能等1000000个first输出完后才会输出second）浏览器是多线程的虽然JS运行在浏览器中，是单线程的，但浏览器不是单线程的。浏览器中很多异步行为都是由浏览器新开一个线程去完成。javascript引擎线程是浏览器多个线程中的一个，它本身是单线程的。浏览器还包括很多其他线程，如界面渲染线程，浏览器事件触发线程，Http请求线程等。所以，所谓的javascript是单线程的，是指javascript运行在浏览器中是单线程的，叫做javascript引擎线程。
用户自定义回调函数，有些时候会在浏览器默认动作之前发生。比如，用户输入框输入文本，keypress事件会在浏览器接受文本之前触发。因此，下面代码无法达到目的：

```
document.getElementById('input').onkeypress = function(){
    this.value = this.value.toUpperCase()
}
上面代码想在用户输入后，立马将字符转换为大写。但实际上，它只能将上一个字符转为大写，因为浏览器此时没有真正接收到文本，所以 this.value 娶不到最新输入的那个字符。这里用 setTimeout 来改写成如下代码才能实现：
```
```
document.getElementById('input').onkeypress = function (event) {
    var self = this;
    setTimeout(function(){
        self.value = self.value.toUpperCase()
    },0)
}
```

setTimeout：在指定的毫秒数后，将定时任务处理的函数添加到执行队列的队尾。
setInterval：按照指定的周期(以毫秒数计时)，将定时任务处理函数添加到执行队列的队尾。

setTimeOut vs setImmediate
https://nodejs.org/zh-cn/docs/guides/event-loop-timers-and-nexttick/#what-is-the-event-loop
队列优先级：
https://segmentfault.com/a/1190000021937507
浏览器引擎与node.js不一样

https://segmentfault.com/a/1190000011198232

### 深浅拷贝

### prototype
http://wendingding.com/2018/04/15/javaScript%E7%B3%BB%E5%88%97%20%5B04%5D-javaScript%E7%9A%84%E5%8E%9F%E5%9E%8B%E9%93%BE/


### CDN加速
https://www.huaweicloud.com/zhishi/cdn001.html

### vue 与 jquery区别
vue和jq最大的区别在于对dom元素的操作，vue基本不涉及dom操作，只注重业务逻辑的操作，而jq要经常涉及dom操作


### webpack vs gulp
gulp强调的是前端开发的工作流程，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。
webpack是一个前端模块化方案，更侧重模块打包，我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。

### 说说vue react angularjs jquery的区别
JQuery与另外几者最大的区别是，JQuery是事件驱动，其他两者是数据驱动。
JQuery业务逻辑和UI更改该混在一起， UI里面还参杂这交互逻辑，让本来混乱的逻辑更加混乱。
Angular，vue是双向绑定，而React不是
其他还有设计理念上的区别等

### 浏览器拿到请求数据后：


### 改写父类prototype

### 前端框架的好处


### 编程范式 in js


### 对称加密 https
https://zhuanlan.zhihu.com/p/96494976

### 单线程js
一、为什么JavaScript是单线程？

JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。那么，为什么JavaScript不能有多个线程呢？这样能提高效率啊。

JavaScript的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？

为了利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程，但是子线程完 
全受主线程控制，且不得操作DOM。所以，这个新标准并没有改变JavaScript单线程的本质。
————————————————
版权声明：本文为CSDN博主「WebCallMeKing」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_36995542/article/details/80007381

webworker:
https://www.w3school.com.cn/html/html5_webworkers.asp


### UMD, AMD, CommonJS
https://zhuanlan.zhihu.com/p/32639434
UMD:
CommonJS和AMD都很流行，但没有达成一致。推动大家寻找一种支持这两者的『通用模式』。这不是别的，正是：通用模块定义(UMD/Universal Module Definition)。
诚然，这种模式是丑陋的，但是兼容AMD和CommonJS，还支持老式『全局』变量定义.
CommonJS:
如果熟悉Node，可能就会熟悉CommonJS的方式(Node用了稍不同版本)。另外，用Browserify实现的CommonJS也得到了广泛的认可。

AMD
异步模块定义(Asynchronous Module Definition)在前端得到广泛认可，RequireJS是最流行的实现。