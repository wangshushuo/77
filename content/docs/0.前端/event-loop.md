# Event Loop

1. 函数调用形成执行栈，执行完弹出。
1. 当执行栈为空时，检查消息队列。
1. 获取第一个消息，调用其绑定的回调函数。此时又循环回第一步。

上面的三部分的循环进行就是Event Loop。

一个事件循环具有一个或多个任务队列。任务队列是一组任务。

当执行栈为空时，会优先检查「微任务队列」。

微任务队列
: 常用的就是Promise

任务队列
: 可以理解为timeout、用户时间、网路请求事件

----
## 研究规范

任务队列是集合，而不是队列[^1]，因为事件循环处理模型的第一步是从所选队列中获取第一个可运行任务，而不是使第一个任务出队。

微任务队列不是任务队列。[^2]

每个事件循环都有一个微任务队列，该队列是一个微任务队列，最初是空的。微任务是一种通俗的方式，指的是通过「queue a microtask」算法创建的任务。

https://html.spec.whatwg.org/multipage/webappapis.html#generic-task-sources

[^1]: Task queues are sets, not queues. [event-loop规范](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop)
[^2]: The microtask queue is not a task queue. [event-loop规范](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop)