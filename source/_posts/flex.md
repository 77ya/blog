---
title: web自适应笔记
date: 2017-06-15 11:41:45
tags:
categories:
---
### web自适应
开始之前，头部需添加以下meta：

		<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
### <font color="#FF7F50">宽度自适应</font>
实现方式一：将外层元素按照百分比铺满的方式，里面的子元素固定或者左右浮动。
![](http://oibijaovc.bkt.clouddn.com/float.png)

		<body>
		<style>
			.div{width: 100%;height: 100px;border:1px solid;}
			.child1{float:left;background-color: pink;width: 50%;}
			.child2{float:right;background-color: #008cee;width: 50%;}
		</style>
			<div class="div">
				<p class="child1">这是左边的</p>
				<p class="child2">这是右边的</p>
			</div>
		</body>

<!-- more -->

实现方式二：Flex布局

justify-content属性介绍：用于设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式。
flex-start|flex-end|center|space-between|space-around|initial|inherit;

align-items 属性介绍：属性定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式。
align-items: stretch|center|flex-start|flex-end|baseline|initial|inherit;

<font color="ffa00">注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。</font>

	<style>
		.box{display:-webkit-flex;display:flex;justify-content:space-between;/* display: inline-flex;行内元素 */align-items:baseline;height: 300px;border:1px solid red;}
		.item{background-color:pink;width:100px;}
	</style>
	<div class="box">
		<span class="item" style="background-color: pink;width: 50px;">注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。</span>
		<span class="item" style="background-color: #008cee;height: 50px;line-height: 50px;">我是的发的发的发</span>
		<span class="item" style="background-color: #ffa000;height: 80px;">我是的发的</span>
	</div>

![](http://oibijaovc.bkt.clouddn.com/flex.png)

实现方式三：box布局

### <font color="#FF7F50">宽度自适应</font>
