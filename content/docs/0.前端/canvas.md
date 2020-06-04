## 学习canvas

```js
var canvas = document.getElementById('tutorial');
var ctx = canvas.getContext('2d');
```
获取到canvas元素，然后通过canvas的api获取到**绘画上下文**。

画矩形
```js
context.fillStyle = 'red';
context.fillRect(x,y,w,h)
```

边框
```js
context.strokeStyle='red';
context.strokeRect(x,y,w,h)
```

画路径
```js
context.beginPath();
context.moveTo(x,y);
context.lineTo(x,y);
context.lineWith=1;
context.strokeStyle="red";
context.stroke();
context.closePath();
```