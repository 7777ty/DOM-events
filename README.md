# DOM事件相关 
1.**什么是事件委托？**
2.**怎么阻止默认事件？**
3.**怎么阻止事件冒泡？**

1. 事件委托又可以叫作事件代理，事件委托就是利用事件冒泡原理，只指定一个事件就可以管理某一类型的所有事件。要想知道什么是事件委托，就要先了解事件冒泡的原理。事件冒泡的原理就是事件从最深的节点开始，逐步向上层的节点传播事件，举个例子：页面有一节点树：div>ul>li>a;如果给最内层的a添加一个点击事件，那么这个点击事件就会一层层向外执行，执行顺序：a>li>ul>div,有这样一个机制，那么如果我们给最外面的div添加点击事件后，在内层的li、ul、div被点击时，都会冒泡到最外层的div上，所以都会触发，这就是事件委托。
2. 在浏览器及互联网发展的过程中，浏览器对许多事件有默认的触发动作，例：点击一个链接-->触发它的url；而如果我们用JS处理一个事件时，通常不需要触发浏览器的默认动作，因此我们需要阻止这些默认事件。
有两种方法可以阻止默认动作：

① 使用event对象，有一个event.preventDefault()方法。
```javascript
//假定有链接<a href="www.baidu.com" id="A">baidu</a>
var a =document.getElementById("A");
a.onclick=function(e){
    if(e.preventDefault){
        e.preventDefault();
    }
}
```
② 使用on<event>(而不是addEventListener)分发处理器，那么我门只要从它的内部返回false即可。
```javascript
<a href="/" onclick="return false">Click Here</a>
``` 
3. 阻止事件冒泡
W3C的方法是e.stopPropogation(),IE使用的是e.cancelBubble=true.
```javascript
window.event?window.event.cancelBubble=true:e.stopPropagation();
```