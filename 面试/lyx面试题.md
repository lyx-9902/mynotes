面试题

## 1 Vue 全家桶介绍

1.项目构建工具、2.路由、3.状态管理、4.http请求工具。

一、Vue-cli是快速构建这个单页应用的脚手架,

二、vue-router  路由

三， vuex为专门为vue.js应用程序开发的状态管理可以理解为全局的数据管理。

四  axios是一个http请求包，vue官网推荐使用axios进行http调用。

## 2  获取select 选中的值

		<form runat="server">
			<select id="select">
				<option value="1">A</option>
				<option value="我是第二个">B</option>
			</select>
		</form>


​		
		var v = document.getElementsByTagName("select")[0].value;
		解析： 每个option都有一个value ，直接获取value

## 3 获取单选框的 选中的值

```
	<form>
	<input type="radio"  name ="fruit" value="apple" checked>苹果
	<input type="radio"  name ="fruit" value="banana">香蕉
	<input type="radio"  name ="fruit" value="pear">梨
	</form>
	
	
	
		document.getElementById('btn_submt').onclick= function(){
				
		 var obj = document.getElementsByName("fruit");
		var value = obj.forEach((item ,index)=>{
				if(item.checked){
					console.log(item.value);
				}})}
				
	解析：item.checked   循环判断			
```

## 4  数组都有哪些方法

```
concat fill  every  find findindex  flat foreach includes indexof join keys pop map push reduce reverse shift  slice some sort tostring unshift values 
```



## 5 对象方法  { }

```
toString()   //返回该对象的字符串表示。 
```

## 6 数组和对象的区别

```
var arr = [1,2,3,4]

var obj = {
	name:'tom',
	hoby:'sing'
}

console.log(arr);

console.log(obj);
```

![1596344888937](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596344888937.png)

区别1： 

数组： Array           有length 属性   可以循环

对象： Object           没有长度  不能循环

​                                                                  对象的方法：

![1596344978144](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596344978144.png)

区别2：调用方法

  arr[1]        数组可以重复

obj.name      对象键值唯一



## 7 数组使用对象的tostring

toString

**使用 call 方法让 obj 对象使用 Object 原型里的 toString() 方法**

改变this的指向，让数组调用Object的to.String方法。





## 8 javascript 中的this

window是js中的全局对象，我们创建的变量实际上是给window添加属性

例子1

```
// function a(){
//     var user = "追梦子";
//     console.log(this.user); //undefined
//     console.log(this); //Window
// }
// window.a();
// 判断： 找函数调用的父级 a函数调用这windown
```

例子2

```
var o = {
    user:"追梦子",
    fn:function(){
        console.log(this); //  this 是 o   打印： 追梦子
    }
}
window.o.fn();   //o是fn的调用者父级

```

例子3

```
var o = {
    a:10,
    b:{
        a:12,
        fn:function(){
            console.log(this.a); //this 指向b   12
        }
    }
}
o.b.fn();
```

总结：

　这里同样也是对象o点出来的，但是同样this并没有执行它，那你肯定会说我一开始说的那些不就都是错误的吗？其实也不是，只是一开始说的不准确，接下来我将补充一句话，我相信你就可以彻底的理解this的指向的问题。

　　情况1：如果一个函数中有this，但是它没有被上一级的对象所调用，那么this指向的就是window，这里需要说明的是在js的严格版中this指向的不是window，但是我们这里不探讨严格版的问题，你想了解可以自行上网查找。

　　情况2：如果一个函数中有this，这个函数有被上一级的对象所调用，那么this指向的就是上一级的对象。

　　情况3：如果一个函数中有this，**这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用，this指向的也只是它上一级的对象**



特殊情况

例子4

```
var o = {
    a:10,
    b:{
        a:12,
        fn:function(){
            console.log(this.a); //undefined
            console.log(this); //window
        }
    }
}
var j = o.b.fn;
j();
```

这里，情况变了。 我们看调用者，  j()   也就是  windown.j()    调用者windown.

this永远指向的是最后调用它的对象，也就是看它执行的时候是谁调用的，例子4中虽然函数fn是被对象b所引用，但是在将fn赋值给变量j的时候并没有执行所以最终指向的是window，这和例子3是不一样的，例子3是直接执行了fn。

## 构造对象的this

```
function Fn(){
    this.user = "追梦子";
}
var a = new Fn();
console.log(a.user); //追梦子
```

这里之所以对象a可以点出函数Fn里面的user是因为new关键字可以改变this的指向，将这个this指向对象a，为什么我说a是对象，因为用了new关键字就是创建一个对象实例，理解这句话可以想想我们的例子3，我们这里用变量a创建了一个Fn的实例（相当于复制了一份Fn到对象a里面），此时仅仅只是创建，并没有执行，而调用这个函数Fn的是对象a，那么this指向的自然是对象a，那么为什么对象a中会有user，因为你已经复制了一份Fn函数到对象a中，用了new关键字就等同于复制了一份。

## **当this碰到return时**

```
function fn()  
{  
    this.user = '追梦子';  
    return {};  
}
var a = new fn;  
console.log(a.user); //undefined
```

再看一个

````javascript
function fn()  
{  
    this.user = '追梦子';  
    return function(){};
}
var a = new fn;  
console.log(a.user); //undefined
````

再来



```javascript
function fn()  
{  
    this.user = '追梦子';  
    return 1;
}
var a = new fn;  
console.log(a.user); //追梦子
```





```javascript
function fn()  
{  
    this.user = '追梦子';  
    return undefined;
}
var a = new fn;  
console.log(a.user); //追梦子
```

什么意思呢？

　　**如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。**



```javascript
function fn()  
{  
    this.user = '追梦子';  
    return undefined;
}
var a = new fn;  
console.log(a); //fn {user: "追梦子"}
```



还有一点就是虽然null也是对象，但是在这里this还是指向那个函数的实例，因为null比较特殊。

```javascript
function fn()  
{  
    this.user = '追梦子';  
    return null;
}
var a = new fn;  
console.log(a.user); //追梦子
```

**知识点补充：**

　　1.在严格版中的默认的this不再是window，而是undefined。

　　2.new操作符会改变函数this的指向问题，虽然我们上面讲解过了，但是并没有深入的讨论这个问题，网上也很少说，所以在这里有必要说一下。



```javascript
function fn(){
    this.num = 1;
}
var a = new fn();
console.log(a.num); //1
```

　　为什么this会指向a？首先new关键字会创建一个空的对象，然后会自动调用一个函数apply方法，将this指向这个空对象，这样的话函数内部的this就会被这个空的对象替代。

**2017-09-15 11:49:14**

　　注意: 当你new一个空对象的时候,js内部的实现并不一定是用的apply方法来改变this指向的,这里我只是打个比方而已.

　　if (this === 动态的\可改变的) return true;



## 9    [JavaScript中call,apply,bind方法](https://www.cnblogs.com/pssp/p/5215621.html)

### call

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user); //追梦子
    }
}

var b = a.fn;
// b() // this 指向windown   windown下没有user.

b.call(a);  //call的同时就是调用。 打印： //追梦子
call只是改变指向。
```

call方法除了第一个参数以外还可以添加多个参数，如下：

```
var a = {
    user:"追梦子",
    fn:function(e,ee){
        console.log(this.user); //追梦子
        console.log(e+ee); //3
    }
}
var b = a.fn;
b.call(a,1,2);
```

### **apply()**

apply方法和call方法有些相似，它也可以改变this的指向

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user); //追梦子
    }
}
var b = a.fn;
b.apply(a);
```

同样apply也可以有多个参数，但是不同的是，第二个参数必须是一个数组，如下：

```
var a = {
    user:"追梦子",
    fn:function(e,ee){
        console.log(this.user); //追梦子
        console.log(e+ee); //11
    }
}
var b = a.fn;
b.apply(a,[10,1]);

-----------------下面也是可以的-但实质都一样------
var b = a.fn;
var arr = [500,20];
b.apply(a,arr);
```

//注意如果call和apply的第一个参数写的是null，那么this指向的是window对象

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this); //Window 
    }
}
var b = a.fn;
b.apply(null);
```

### **bind()**

bind方法和call、apply方法有些不同，但是不管怎么说它们都可以用来改变this的指向。

先来说说它们的不同吧。

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user);
    }
}
var b = a.fn;
b.bind(a);
```

我们发现代码没有被打印，对，这就是bind和call、apply方法的不同，实际上bind方法返回的是一个修改过后的函数。

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user);
    }
}
var b = a.fn;
var c = b.bind(a);
console.log(c); //fn
c() // 追梦子
```

ok，同样bind也可以有多个参数，并且参数可以执行的时候再次添加，但是要注意的是，参数是按照形参的顺序进行的。

```
var a = {
    user:"追梦子",
    fn:function(e,d,f){
        console.log(this.user); //追梦子
        console.log(e,d,f); //10 1 2
    }
}
var b = a.fn;
var c = b.bind(a,10);
c(1,2);

```

## 总结：

call和apply都是改变上下文中的this并立即执行这个函数，bind方法可以让对应的函数想什么时候调就什么时候调用，并且可以将参数在执行的时候添加，这是它们的区别，根据自己的实际情况来选择使用。

https://www.cnblogs.com/pssp/p/5215621.html



## 10 数组去重

方法1

```
// 最简单数组去重法
/*
* 新建一新数组，遍历传入数组，值不在新数组就push进该新数组中
* IE8以下不支持数组的indexOf方法
* */
function uniq(array){
    var temp = []; //一个新的临时数组
    for(var i = 0; i < array.length; i++){
        if(temp.indexOf(array[i]) == -1){
            temp.push(array[i]);
        }
    }
    return temp;
}


var aa = [1,2,2,4,9,6,7,5,2,3,5,6,5];
console.log(uniq(aa));
```

方法2   

es6  Set数据结构

````javascript
var arr = [40, 100,40];

var newdata = new Set(arr) //返回一个对象

console.log( Array.from(newdata));  //返回一个数组

// 结果: 经过转换, 达到去重的目的.   ,
// 唯独IE系列不支持。
````

[ES6，Array.from()函数的用法](https://www.cnblogs.com/kongxianghai/p/7417210.html)

ES6为Array增加了from函数用来将其他对象转换成数组。

当然，其他对象也是有要求，也不是所有的，可以将两种对象转换成数组。

1.部署了Iterator接口的对象，比如：Set，Map，Array。



### 数组 排序  **sort()**jquery

```
var points = [40, 100, 1, 5, 25, 10];

var newdata =points.sort(function(a, b){return a - b}); 

console.log(newdata); //(6) [1, 5, 10, 25, 40, 100]



```

## 11 [常见的js 里对数字进行处理的函数方法集合](https://www.cnblogs.com/qianmojing/p/6258067.html)

常见的对小数值舍入为整数的几个方法：Math.ceil()、Math.floor()和Math.round()。 这三个方法分别遵循下列舍入规则：

Math.ceil()执行向上舍入，即它总是将数值向上舍入为最接近的整数；

Math.floor()执行向下舍入，即它总是将数值向下舍入为最接近的整数；

Math.round()执行标准舍入，即它总是将数值四舍五入为最接近的整数(这也是我们在数学课上学到的舍入规则)。

Math.abs()返回数的绝对值，Math.abs(4)||Math.abs(-4) 都返回4；

parseInt() 函数可解析一个字符串，并返回一个整数。

parseFloat() 函数可解析一个字符串，并返回一个浮点数。该函数指定字符串中的首个字符是否是数字。如果是，则对字符串进行解析，直到到达数字的末端为止，然后以数字返回该数字，而不是作为字符串

Number() 函数把对象的值转换为数字。如果不是数字则返回NaN;



1.会四色五入

```
var` `num =2.446242342;
num = num.toFixed(2); ``// 输出结果为 2.45
```

12 [前后端分离与前后端不分离的区别](https://www.cnblogs.com/skaarl/p/9658114.html)

在前后端不分离的应用模式中，前端页面看到的效果都是由后端控制，由后端渲染页面或重定向，也就是后端需要控制前端的展示，前端与后端的耦合度很高。

这种应用模式比较适合纯网页应用，但是当后端对接App时，App可能并不需要后端返回一个HTML网页，而仅仅是数据本身，所以后端原本返回网页的接口不再适用于前端App应用，为了对接App后端还需再开发一套接口。

分离：

后端仅需开发一套逻辑对外提供数据即可。

## 12  计时器

```
 setTimeout("alert('对不起, 要你久候')", 3000 )
```

window.setInterval()方法        循环

window.setTimeout()方法，    一次

清除方法：

分别是window.clearInterval()  和   window.clearTimeout()。

## 13 JavaScript数据类型

**JavaScript 数据类型**
**6 种**不同的数据类型：
       String                字符串     String  ' '  引号包裹的内容
       number
       Boolean
       object
       function
        symbol     es6数据类型
**3 种**对象类型：
       Object      {  }  对象
       Date
       Array          [ ]  数组
**2 种**不包含任何值的数据类型：
       Null
       undefined

+++++++++++++++++++++++++++分割线++++++++++++++++++++++++++++++++

js 中的数据类型总体来说分为两种，他们分别是：值**类型** 和 引用**类型**

- **值类型（基本类型）**：数值型（Number)，字符类型（String），布尔值型（Boolean），null 和 underfined
- **引用类型（类）**：函数，对象，数组等

**值类型理解：**变量之间的互相赋值，是指开辟一块新的内存空间，将变量值赋给新变量保存到新开辟的内存里面；之后两个变量的值变动互不影响

+++++++++++++++++++++++++++分割线++++++++++++++++++++++++++++++++

**1、基本数据类型和引用数据类型**

　　ECMAScript包括两个不同类型的值：基本数据类型和引用数据类型。

　　基本数据类型指的是    简单的数据段，引用数据类型指的是有    多个值构成的对象。

　　当我们把变量赋值给一个变量时，解析器首先要确认的就是这个值是基本类型值还是引用类型值。

https://www.cnblogs.com/cxying93/p/6106469.html

```
常见的基本数据类型：

　　Number、String 、Boolean、Null和Undefined。基本数据类型是按值访问的，因为可以直接操作保存在变量中的实际值。示例：

　　var a = 10;

　　var b = a;

　　b = 20;

　　console.log(a); // 10值
```





下面为大家介绍5种简单的基本类型：
1.字符串(String)类型



## Undefined（未定义）

一个变量没有赋值就是undefined
同前面的类型不一样的是，这里的未定义是没有等号的，即未赋值

```
var unde;
alert(typeof unde);   //Undefined

```

## Null（空）

*注：一种特殊的Object类型 为空 弹出object

```
var nl = null;
alert(typeof null);   //Object
```

## Undefined 和Null**区别**：

Undefined：未定义会存进去，但它没有值，会占用内存
Null：空 不会存里面，只是一个空，不存在，因而不会占内存
因此，Undefined 这个值表示变量不含有值。可以通过将变量的值设置为 null 来清空变量。





12

# 14 . JS中浅拷贝和深拷贝的区别

浅拷贝： 拷贝一层，两个数据指向同一个地址，一个修改，另一个也被动修改。

1、什么是浅拷贝

创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。

2、什么是深拷贝

深拷贝会拷贝所有的属性，并拷贝属性指向的动态分配的内存。当对象和它所引用的对象一起拷贝时即发生深拷贝。深拷贝相比于浅拷贝速度较慢并且花销较大。拷贝前后两个对象互不影响。

```
//再举个栗子
let a = [0,1,2,3,4];
let b = a;
console.log(a===b,a==b);
a[0] = 1;
console.log(a,b);

//得到结果：
/*
true true
[ 1, 1, 2, 3, 4 ] [ 1, 1, 2, 3, 4 ]
*/
//只修改了a的值，b却也跟着一起修改了

//首先我定义了一个数组复制给a，那么此时在栈区就会存在一个名为a，值为该数组存在堆区的地址，
//当我们再将a复制给b时，这时在栈区又生成了一个名为b但值指向的地址和a是相同的
//所以在我们修改a的同时，由于b的值也指向该地址，所以b也一起更改了

//那我们如何解决浅拷贝带来的问题呢？拷贝值的同时生成新的地址
//在这里博主举了几个深拷贝的方法

/*		
		//方法一：转换成JSON字符串指向新的内存地址
/		/let demo = JSON.stringify(e);
        //arr.push(JSON.parse(demo));
        
        //方法二：Jquery的extend方法也可以实现深拷贝
        
        //方法三：Lodash中的clone和cloneDeep方法也可以实现深拷贝
*/

//再提供一个Lodash数组分页的实例
```

#### jQuery clone() 方法

克隆所有的 <p> 元素，并插入到 <body> 元素的结尾：

```
$("button").click(function(){
    $("p").clone().appendTo("body");
});
```

深拷贝

```
function extendDeep(parent, child) {
var i,
proxy;
proxy = JSON.stringify(parent); //把parent对象转换成字符串
proxy = JSON.parse(proxy) //把字符串转换成对象，这是parent的一个副本
child = child || {};
for(i in proxy) {
if(proxy.hasOwnProperty(i)) {
child[i] = proxy[i];
}
}
proxy = null; //因为proxy是中间对象，可以将它回收掉
return child;
}

```

```
var dad = {
counts: [1, 2, 3],
reads: {paper: true}
};
var kid = extendDeep(dad);
//修改kid的counts属性和reads属性
kid.counts.push(4);
kid.reads.paper = false;
console.log(kid.counts); //[1, 2, 3, 4]
console.log(kid.reads.paper); //false
console.log(dad.counts); //[1, 2, 3]
console.log(dad.reads.paper); //true

```

15 