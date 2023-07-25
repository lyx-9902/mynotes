# 1.layer open

```js
top.layer.open({
			type: 2,
			title: false,
			shadeClose: true,
			area: ['80%', '90%'],
			content: 'page/kshdp/tbgl-xiazuan.html?ID=' + id + '&SJXZLX=' + SJXZLX,
			closeBtn: 1
		});
```
```js
layer.open({
			type: 2,
			title: false,
			shadeClose: true,
			area: ['80%', '90%'],
			content: 'page/kshdp/tbgl-xiazuan.html?ID=' + id + '&SJXZLX=' + SJXZLX,
			closeBtn: 1
		});

传参方式
url='./page/kshdp/tbpz/tbsz-echarts2.html?ID='+ZID+"&name="+echartsTitle;
```

# 2.1  弹窗关闭

```
2.1 	

function fn(){
	var index = parent.layer.getFrameIndex(window.name); //先得到当前iframe层的索引
	console.log(index)
	parent.layer.close(index); //再执行关闭  	
		}
```



# 2.禁用事件




```html
 <div class="add_icton_aniu" style="pointer-events: none;">  禁用事件
```

# 3. layui关闭当前弹窗   并刷新父页面

```
 var index = parent.layer.getFrameIndex(window.name);
                    parent.layer.close(index);
                    
 parent.window.$("iframe").attr("src",'page/mhgl/ksh_wdgl.html')
 
 
 parent.location.href='zhibiaofabu.html?YMID='+ ymid +'&YMMC='+ ymmc +'&BJZT=1';  //重定向 有刷新功能
```



# 4.操作父元素的dom

```
parent.window.$('.layui-layer-title').css({'color':'black'})
```

# 5.循环获取attr 属性值

```
$('input[name=' + key + ']').attr("value", map[key]);
```

# 6.改变父页面的locatin href地址

```
parent.location.href='zhibiaofabu.html?YMID='+ ymid +'&YMMC='+ ymmc +'&BJZT=1';


parent.layer.open({ //表示在父页面层级上打开  就是本页的上一级
		type:2,
		content:dUrl,
		title:false,
		area:['100%','100%']
	})
//经测试：window.location.href与location.href,self.location.href,location.href都是本页面跳转
     top.location.href='http://www.baidu.com'; 是最外层的页面跳转"的意思。

```

# 7.父页面刷新/当前的页面刷新

```
layer.msg(res.message,{time:1000},function(){

​			parent.layer.closeAll();  //父页面关闭弹窗

​			parent.location.reload();//父页面刷新

​		});

当前的页面刷新

window.location.reload();


layer.msg(res.message,{time:1000},function(){
				parent.layer.closeAll();
				parent.location.reload();
			});
```

# 8.模仿自适应 

```
  $(".wrap").css("height", $(window).height());//模仿自适应  
    var aaa = ($(window).height() - $(".bg").height()) / 2;
    $(".bg").css("top", aaa);

```

# 9.eval() 函数 字符串计算

```
4.eval() 函数
  eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码。
 语法   eval(string)
```

# 10 layer.open title 样式

```
	parent.layer.open({
	  	type: 2,
	  	title: [name+"详情","font-size:16px;text-align:center;background:#4f87da;color:#ffffff;font-weight:bold;border:0;"],
	  	shadeClose: true, //点击遮罩关闭层
	  	fix: false, //不固定
	  	area: ['60%','75%'],
	  	content: url
	});
```





