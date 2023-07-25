# 第十二天

http://hemin.cn/jq/  jq手册

函数整体提升；变量生命提升。

var a =10;    加分号  函数不加分好，因为有{}； 10就是变量，存放于内存中。

## 1.入口函数

```
		window.onload=function(ev){
			console.log(ev)
		}
		
		$(document).ready(function(){
			alert(0)
		})
	区别：
1.原生js等到dom和img都加载完毕后才会执行；jq只会等到dom加载完毕，影响到拿dom节点。
2. 原生 多个会覆盖
   jq 不会覆盖 顺序执行
```

$.hod



## 2.自执行函数  和 $.holdReady(true)

```
1.(function test(){alert(0)})()

2.
		$.holdReady(true)
		
		$(document).ready(function(){// 页面加载完毕自动执行。
			alert(0)
		})
		
		$.holdReady(false)//  可以方法点击事件中控制加载顺序和时间

```

## 3.jquery 冲突 $

```
放弃$使用权；或者是重新定义一个。

var my$ = jQuery.noConflict();
		my$(function(){
			alert(0)
		})
```

## 4.jq  获取的dom序列组 是一个伪数组

```
获取3个lidom,打印出来类似数组
有0-2下标，有length属性。


```

## 5.静态方法和实例方法Aclass

```

//1. 定义一个类
function Aclass(){}
//2.给类加上静态方法
Aclass.stacMethod=function(){alert(0)}
//静态方法通过类名调用
Aclass.stacMethod()

//1. 给类添加一个实例方法
Aclass.prototype.instanceMethod=function(){console.log(0)}

//实例方法通过累的实例调用
var a = new Aclass();
a.instanceMethod()


```

## 6.jq $.each

```
		两个参数：一个原数组，一个回调函数 （index  和item)
		
		var arr2 =	$.each(arr,function(index,value){
			console.log(index,value)
		})
		console.log(arr2)
0 "小0" 
1 "小1" 
2 "小2"
Object {0: "小0", 1: "小1", 2: "小2", length: 3} 
 1.不支持return 数据处理
2. arr2  each 默认遍历谁就返回谁
3. 数组 对象都可以

定义和用法
each() 方法规定为每个匹配元素规定运行的函数。

提示：返回 false 可用于及早停止循环。
```



## 7.原生 forEach 

```
	var arr = [11, 22, 33, 44, 55]

		var obj = {//伪数组
			0: '小0',
			1: '小1',
			2: '小2',
			length: 3
		};
		
arr.forEach(function(value ,index){
	if(value=='xiaoming'){console.log(value)}
//	console.log(value ,index)	
})
只能处理数组，不能return 没有返回值。为每个 项执行一遍。

```





## 8.  原生和jq  的  map

```
	var arr = [11, 22, 33, 44, 55]

		var obj = {//伪数组
			0: '小0',
			1: '小1',
			2: '小2',
			length: 3
		};
1.原生map
	var newarr=	arr.map(function(value, index, oarr) {
			      
					console.log(value,index, oarr)
					   return value+index
			})
console.log(newarr)//返回新数组[11, 23, 35, 47, 59] 
//原生map 参数:一个函数   3个参数  
value, idnex, oarr  循环的 元素 下标  arr数组
和原生ecah一样
不能遍历伪数组
2.jquery

	var arr1 =	$.map(arr,function(value,index){
			console.log(value, index)
			return value+index
		})
		console.log(arr1)
		//jq的map传入两个参数 一个是原数组，一个是回调。回调中参数一个元素，一个索引和原生ecah一样
		可以遍历伪数组
总结： 
1.两个传参不一样，
2.jq map可以遍历伪数组 和对象 
3.当回调函数没有return； 原生返回的 
[undefined, undefined] 
jq返回的 []


```

## 9.trim   去除str两边留白

```
var  str ='       na  m   '
var  newstr= $.trim(str)
console.log('---'+newstr+"---")
注意：只能去除两边，中间的不行。

```

## 10 . $.isArray

```
		var  obj = [1, 2, 3, 4]
		var res = $.isArray(obj)
		console.log(res)//true 
//		可以区分伪数组 对象 

```

## 11 $.isFunction()

```

$.isFunction() //判断是否为方法
```

## 12 isNaN

```
if(isNaN(value)) return;
判断是否为nan  return后，后面的代码不再执行。


```



# 属性

### 1.内容选择器

```
		<div class="">包含   </div>
		<div class="">包含dsfdsf   </div>


var $div=$("div:contains('包含')")  //
		    console.log($div)


```

### 2  包含 指定子元素 标签 选择器

```
		
	        <div><p>Hello</p></div>
		
		console.log(    $("div:has(p)")    )
```

# 属性选择器

```
         <div name='a'></div>
		console.log(  $("[name='a']")      )
```

## 1.获取属性值 和设置

```
1.<div name='a'></div>
 var aa=$("[name='a']") .attr('name') //获取dom上的属性值
	
2.$("[name='a']") .attr('name',"newname") //获取dom上的属性值
<div name='a'></div>
传入一个参数是获取，两个参数是更换
3.移除属性
	$("[name='a']") .removeAttr('name') 
同时删除dom多个属性  class也是属性
  	$("[name='a']") .removeAttr('name class') 
```

- [prop(n|p|k,v|f)](http://hemin.cn/jq/prop.html)
- [removeProp(name)](http://hemin.cn/jq/removeProp.html)

## 2.  prop   判断input是否选中

```js
功能和attr相似
<input type="checkbox" name="" id="" checked value="" />


//		官方推荐:操作节点时具有true 和false 另两个属性的属性节点 如checked,selected ,disableed
//		使用prop()  ,其他的使用attr()

  $("input[type='checkbox']").prop("checked" ,false)   
    
```

# css类 

```
addClass(class|fn)
removeClass([class|fn])
toggleClass(class|fn[,sw])

$('.div').click(function(){
			$('.div').toggleClass("active")
	})


```

### 1.HTML代码/文本/值

```

html([val|fn])
text([val|fn])
val([val|fn|arr])


```

### 2.jq 获取和设置 css

```

   	$("div").css('height') 
 $("div").css('height','200px') 
 获取节点： 一个值是获取；两个值是设置。
 
 
```

### 3.width 获取宽和设置宽

```
 
 $("div").width('100px') 
console.log(  $("div").width()  )


```

### 4. offset获取宽和设置宽



```

	距离窗口的数值 ； top  left两个参数
	$("div").offset().top
	
		$("div").offset({
			top:500,
			left:500
		})
		

```

### 5.获取网页滚动距离

```

考虑到浏览器兼容

$("button").click(function(){
			console.log($("html").scrollTop() +                          $("body").scrollTop())
		})
		
	加入数值是设置
    console.log($("html").scrollTop(300) + $("body").scrollTop(300))
		
		
		
		
		
```

# 事件

```
页面载入
ready(fn)
事件处理
on(eve,[sel],[data],fn)1.7+
off(eve,[sel],[fn])1.7+
bind(type,[data],fn)
one(type,[data],fn)
trigger(type,[data])
triggerHandler(type, [data])
unbind(t,[d|f])
事件委派
live(type,[data],fn)1.7-
die(type,[fn])1.7-
delegate(s,[t],[d],fn)
undelegate([s,[t],fn])
事件切换
hover([over,]out)
toggle([spe],[eas],[fn])1.9-
事件
blur([[data],fn])
change([[data],fn])
click([[data],fn])
dblclick([[data],fn])
error([[data],fn])
focus([[data],fn])
focusin([data],fn)
focusout([data],fn)
keydown([[data],fn])
keypress([[data],fn])
keyup([[data],fn])
mousedown([[data],fn])
mouseenter([[data],fn])
mouseleave([[data],fn])
mousemove([[data],fn])
mouseout([[data],fn])
mouseover([[data],fn])
mouseup([[data],fn])
resize([[data],fn])
scroll([[data],fn])
select([[data],fn])
submit([[data],fn])
unload([[data],fn])
```

## 事件解绑 .off()

```
不传入参数，移除dom所有事件；
传入一个类型， 移除一类。
传入两个 移除指定事件

$("button").off()
$("button").mouseover(function() {
						$("button").off('click')
					})
					
					
$("button").mouseover(test1)
$("button").off('click',test1)

```

## 触发trigger

```
	作用是： dom上如果有事件，trigger传入指定类型后，会自动触发。
	例如下面mouseover就回出发点击事件
    
    $("button").click(function() {
			console.log(0)
		})

				$("button").mouseover(function() {
					$("button").trigger('click')
					})
					
					
	$("button").triggerHandler('click')	
    triggerHandler，触发son的事件，不会触发father的事件。 就是不会冒泡，和 submi的默认行为。
    a标签特殊
```

## 自定义事件的触发

```
自定义事件的触发    自定义名字myclick 
				1.事件必须通过on绑定
				2.事件必须通过trigger来触发.
				
				$("son").on('myclick',function(){
					//事件
				})
				$("son").trigger('myclick')


```

## 事件命名空间click.name1

```
	场景： 同一个dom，两个人同时都写了一个点击事件， 点击时都会触发，为了区分，可以采用此方法。
	
	$("son").on('click.name1',function(){
					//事件
				})
				$("son").trigger('click.name1')
```

## 事件委托delegate  /类似与on

```

场景： ul 中 后期添加li标签，同时保证li标签上有事件。
$("ul").delegate("li","click",function(){
//daima
});
```

# 动画

## 1.show

```
用于display：none的元素
参数一个时间，一个回调。
$('button').click(function(){
				$('.img').show(2000,'swing',function(){
					console.log('加载玩了')
				})
		})
```

## 2.slideDown 

```
一个放，一个收，一个切换。使用场景：菜单下拉和收拢

slideDown([s],[e],[fn])
slideUp([s,[e],[fn]])
slideToggle([s],[e],[fn])


$('button').click(function(){
				$('.img').slideToggle(1000,function(){
				
				})
		})
		
		
引入一个： dom.stop()   防止动画异常，执行 动画前先暂停之前的。		
		
```

3.淡入淡出

```

fadeIn([s],[e],[fn])
fadeOut([s],[e],[fn])
fadeTo([[s],o,[e],[fn]])
fadeToggle([s,[e],[fn]])
```

自定义动画 animate

```
	<button id="go"> Run</button>
   <div id="block">Hello!</div>


$("#go").click(function(){
  $("#block").animate({ 
    width: "90%",
    height: "100%", 
    fontSize: "10em", 
    borderWidth: 10
  }, 1000 );
});

```

## 动画延迟delay

```
两个动画中间的延迟

$('#foo').slideUp(300).delay(800).fadeIn(400);

```

# 第十三天



# 文档处理

## 1.内部插入外部插入

```
内部插入
append(content|fn)
appendTo(content)
prepend(content|fn)
prependTo(content)

外部插入
after(content|fn)
before(content|fn)
insertAfter(content)  页面上的两个节点调整前后顺序
insertBefore(content)


包裹
wrap(html|ele|fn)
unwrap()
wrapAll(html|ele)
wrapInner(html|ele|fn)




1. appendTo
	<ul>
			<li>第1个</li>
			<li>第2个</li>
			<li>第3个</li>
		</ul>
		
		
		$('<li>第3个</li>').appendTo($('ul'))
			$('ul').prepend($('<li>第新加的个</li>'))
			
			// 外部的
			// 外部的后面
			$('ul').after($('<li>第新加的个</li>'))
           // 外部的前面
          $('ul').before($('<li>第新加的个</li>')) 
2.前后调换位置          
     <p>I would like to say: </p>
		<div id="foo">Hello</div>
        
       $("p").insertAfter("#foo"); 
```

## 2.删除节点

```
empty()
remove([expr])

detach([expr])
        $("p").remove()//移除节点 包含本身
		$(".active").remove()//移除节点
		$("p").empty()()//清空节点内部  节点本身保留


```

## 3.替换节点

```
replaceWith(content|fn)
replaceAll(selector)

		var $h6=$('<p>pppp</p>')
	   $('h1').replaceWith($h6)//用新节点替换h1
		$h6.replaceAll ('h1')//用新节点替换所有h1
```

## 4. 复制clone

```
clone([Even[,deepEven]])
将ul 的第一个li， 复制到ul的后面。
浅复制，仅仅复制dom, 
true深复制， li标签的 点击事件也可以复制过去。


       var $li=$('li:first').clone(false)
	        $("ul").append($li)


```

# 音乐播放器

## css

```
音乐播放器的背景 高斯模糊
1.
.box{
	background: url(00.jpg);
	filter: blur(100px);//数值越大 ，背景图片月模糊。
}
2.
jq的hover事件， 底层时通过mouseover  mouseleave，所以在事件on委托绑定的时候，必须替换。 不能使用hover


```

## return

```

	if(isNaN(value)) return;  后面代码不再执行。
	
	
	if(res==null) return true;
	代表，此次如果是null ,那么继续下一次循环


```

