今天学习了使用原生js来实现拖拽
重点记录如下：
1. 拖拽模拟：mousedown mousemove mouseup
> 拖拽体验：在要移动的元素上，按下鼠标的左键，移动鼠标，元素跟着鼠标移动实现拖拽

3. 涉及的样式?
> 盒子定位


1. 确定盒子位置公式的原理
   ```js
   ev.pageX
   ev.pageY 这连个是鼠标在页面上的位置

   box.offsetWidth
   box.offsetHeight 盒子距离父级别参照物的距离
   
   唯一不变的就是，鼠标在box上的开始按下的点距离盒子左上角的位置.
   公式 
   
   移动后鼠标位置 - 移动后box的offset值 = 移动前的鼠标位置 - 移动后box的offset值
   ```
   
2. 如何防止鼠标丢失?

   >
   >
   >在document上来绑定事件，这样鼠标就不会跑出去了..............





 ### 全部代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./css/reset.min.css">
    <style>
        html,
        body {
            height: 100%;
            overflow: hidden;
        }
        
        .box {
            position: absolute;
            top: 0;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: red;
            cursor: move;
            font-size: 16px;
            text-align: center;
            line-height: 100px;
        }
    </style>
</head>

<body>
    <!-- 盒子的父级参照物是body -->
    <div class="box" id="box">box</div>
    <script>
        // 将值存在自定义属性上
        box.onmousedown = down;


        function move(ev) {
            // 随时获取当前鼠标的信息，计算盒子的最新位置
            let curL = ev.pageX - this.startX + this.startL,
                curT = ev.pageY - this.startY + this.startT;
            let HTML = document.documentElement,
                minL = 0,
                minT = 0,
                maxL = HTML.clientWidth - this.offsetWidth,
                maxT = HTML.clientHeight - this.offsetHeight;

            // 边界判断 (0,HTML.clientWidth - this.offsetWidth)
            // (0,HTML.clientHeight - this.offsetHeight)
            curL = curL < minL ? minL : (curL > maxL ? maxL : curL);
            curT = curT < minT ? minT : (curT > maxT ? maxT : curT);
            this.style.left = curL + "px";
            this.style.top = curT + "px";

        }

        function down(ev) {
            // 存储鼠标起始位置的信息和盒子的起始位置存储在盒子的自定义属性上
            this.startX = ev.pageX;
            this.startY = ev.pageY;
            this.startL = this.offsetLeft;
            this.startT = this.offsetTop;
            // 鼠标按下的时，给mousemove和mouseup绑定方法
            // 使用bind绑定this为当前元素
            document.onmousemove = move.bind(this);
            document.onmouseup = up.bind(this);
            // this.setCapture(); // chrome不支持

        }

        function up(ev) {
            // 鼠标抬起，将move和up的方法绑定的方法移除
            document.onmousemove = null;
            document.onmouseup = null;
        }
    </script>
</body>

</html>
```

