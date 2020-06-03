# JS相关问题

## 1. 请解释事件代理 (event delegation)。
{{< details "解答" false >}}
比如有`body>div>button`，事件代理就是在一个高级元素（body）上绑定一个事件处理函数处理其子元素，利用了事件冒泡机制。

好处节省内存和事件。因为事件处理函数就是一个对象，对象会占用内存，绑定处理函数也会花费事件。

延伸
{{< /details >}}

## 2. 请解释 JavaScript 中 this 是如何工作的。
{{< details "解答" false >}}
this指向函数运行时所在的对象，而不是创建时。

比如，对象a的b属性是一个函数，其中打印this。当调用a.b()时打印的是对象a。如果把a.b赋值给一个变量c，在调用c，则打印出来的this是全局变量window。
![this](/image/this-1.jpg)

当函数作为对象的方法时，this指向对象。当直接调用函数时，this指向全局变量。
{{< /details >}}