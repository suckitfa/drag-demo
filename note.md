- HTML5中的拖拽事件
> dragstart / drag/ dragend
> dragenter / dragleave/ dragover
> drop

- 基于原生JS实现拖拽

<!-- setCapture
releaseCapture
在chrome不支持 -->

<!-- 谷歌浏览器中解决焦点丢失问题 -->
<!-- 给document绑定 -->
<!-- this为document,如何解决？ -->


# 鼠标失去焦点问题解决方案？
问题描述:


只能够慢慢的移动？移动快了盒子不动了，**电脑计算来不及了**
”动的再快也逃不出如来的手掌心“
所以给document绑定鼠标移动事件，同时使用bind来绑定当前的元素