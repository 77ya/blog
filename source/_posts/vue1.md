---
title: 初识vue
date: 2017-09-20 23:10:57
tags: Vue
categories: programming
---

vue data 的简单操作

<!-- more -->

	  export default {
	  name: 'hello123',
	  data() {
	    return {
	      name: '王小二',
	      age: 0,
	      sex: '女',
	      status: true,
	      url: 'https://www.baidu.com/',
	      fn1: function() {
	       alert(假数据)
	      },
	      class1: true,
	      class2: false,
	      classobj: {
	        active: true,
	        'tex2': true
	      },
	      lists: [
	        { color: 'yellow' },
	        { color: 'blue' },
	        { color: 'red' }
	      ],
	      result:['王一','网二','网顺丰速递']
	    }
	  },
	  computed:{
	    myfn:function(){
	      return this.name + "生命周期呀"
	    }
	  }
	}

 
> 模板基础语法

##### 简单数据绑定 #####

 	<p>{{name}}</p>

#### v-if  (问题：age=5，输出10到20之间) #### 

	<p v-if="age>20">年级大于20——{{age}}</p>
    <p v-else-if ="9<age<19">10到20之间——{{age}}</p>
    <p v-else>年龄小于10—— {{age}}</p>

##### 表达式 #####

	<p>{{ status ? '显示' : '不显示' }}</p>

##### v-bind:href 更新属性#####

	 <a v-bind:href='url'>点击这里调到百度去</a>

简写 ：href='url'

##### v-on:click 监听dom #####

	<button v-on:click='fn1'>点击我</button>

简写 @click='fn1'

##### v-for #####	
	
	<p v-for = '(list,index) of lists' v-bind:key='list.color'>
      {{list.color}}_{{index}}
    </p>

for循环中使用key属性： 数据中有id绑定id，无直接绑定index

#### 生命周期 ####

	<p>{{myfn}}</p>

> 计算属性和观察者

#### 计算属性（对data里的数据进行操作） ####

	 computed:{//这是计算属性（对data中的数据进行处理）
	    myfn:function(){
	      return this.name='计算属性操作name';
	    }
	  }


#### 方法 ####

#### 问题：值绑定复选框逻辑值设置为字符串，失败， ####

解决方案：在data数据中传值，不可直接在html写字符串
  <input type="checkbox" v-model='checkbox1' v-bind:true-value='name' v-bind:false-value='sex'>

#### es6中export的用法： #### 
[参考地址](http://www.php.cn/js-tutorial-357671.html)

export用于对外输出本模块（一个文件可以理解成一个模块）变量的接口————对外输出（导出）

import用于在一个模块中加载另一个含有export接口得模块————加载

也就是说使用export命令定义了模块的对外接口以后，其他js文件可通过import命令加载这个模块

如下：（a、b文件在同一目录下）

a.js
	
	var sex = "boy";
	var echo = function(value){
		console.log(value)
	}
	export {sex,echo}
	//通过向大括号中添加sex，echo变量并且export输出，就可以将对应变量值以sex、echo变量标识符形式暴露给其他文件而被读取到

	//不能写成export sex这样的方式，如果这样就相当于export "boy",外部文件就获取不到该文件的内部变量sex的值，因为没有对外输出变量接口,只是输出的字符串。

b.js
	
	//通过import获取a.js文件的内部变量，{}括号内的变量来自于a.js文件export出的变量标识符
	
	import {sex,echo} from "./a.js"
	console.log(sex) // boy
	console.log(echo(sex)) // boy

用export和import时，用户必须知道a.js所暴露的变量标识符（sex，echo），否则无法加载。

而export default命令，为模块指定默认输出，这样就不需要知道所要加载模块的变量名。

a.js

	var sex = "boy";
	export default sex //sex不能加大括号
	//原本直接export sex外部是无法识别的，加上default就可以了.但是一个文件内最多只能有一个export default。

	//其实此处相当于为sex变量值"boy"起了一个系统默认的变量名default，自然default只能有一个值，所以一个文件内不能有多个export default。

b.js
	
	本质上，a.js文件的export default输出一个叫做default的变量，然后系统允许你为它取任意名字。所以可以为import的模块起任何变量名，且不需要用大括号包含
	import any from "./a.js"
	import any12 from "./a.js"
	console.log(any,any12) // boy,boy

具体使用

1、

demo1.js
	
	export const str = "htllo world";
	export function f(a){
		return a+1;
	}

对应的导入方式：

demo2.js

	import {str,f} from "./demo1.js" //可以分开两次写，导入的时候带花括号

2、

demo1.js

	export default const str = "hello world"

demo2.js

	import str from "./demo1.js" //导入时没有花括号
 
#### 创建局部组件时，只在父组件中可用，父组件是什么？为生效  ####

整个导出的对象是父组件
	export default {
		data:'',
		component:{
			'test':my-test //标签名+组件名  这个是子组件
		}
	}

#### prop怎么传数据 ####

已解决：父组件向子组件传数据，肯定是现在父组件中拿数据
 
组件实例的作用域是孤立的——所以不能在子组件的模板内直接引用父组件。

prop：父组件向子组件传数据，prop是支撑的意思，父亲是家里的支撑，所以数据写在<child message='这是父组件数据'></child>

注意：驼峰式命名的prop需要转换为短横线分隔式命名：myMessage转换为my-message


#### Prop 把一个对象的所有属性作为prop传递  子组件props里应该怎么写 ####
#### 单项数据刘 定义一个局部变量 如何执行 ####

已解决
	 data:function(){
	            return {
	                door:'数据测试',
	                counter:1,
	                name:'小彭子',
	                age:'18'
	                //newprop: this.myprop //将传过来的全局变量转为局部变量
	            }
	        },

#### prop从父组件传对象时失败 ####
#### prop从父组件传递字符串弹出警告，但是成功了 ####
#### 非prop特性 哪里下载组件 ####
#### $emit(自定义事件名)触发子组件的同时触发父组件绑定事件 ####

	var result = value.trim() //去除str前后空格
	.slice(0,value.indexOf(".") === -1
	       ? value.length
	       : value.indexOf(".")+3 //保留两位小数
	      )




#### 视频笔记 ####

- “数据双向绑定”适用于表单元素 
- 脚手架工具、webpack、组件化开发

#### scoped ####


于我们使用的scoped属性，它的存在可以让我们的组件的样式保持独立性，但同时使用scoped也存在一个问题，就是我们不应该在项目中定义重复的样式规则名称

	<style scoped></style>

#### computed ####

页面当中展示的数据需要尽快处理后展示



