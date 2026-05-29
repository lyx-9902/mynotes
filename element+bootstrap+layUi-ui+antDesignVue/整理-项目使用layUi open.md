## 五种弹窗类型

0 dialog **信息框** 默认  ，同时只能存在一个层；

1 page **页面层**， 可同时存在多个层

2 iframe **内联框架层** 可同时存在多个层

3 loading **加载层** 同时只能存在一个层

4 tips **贴士层** 可配置同时存在多个层

​    页面中弹窗操作，一版使用1 2， 内容少的使用1，拼接字符串dom;内容多的使用2.（url？xx=xx传递参数）

[2层弹窗案例](https://blog.csdn.net/sunsineq/article/details/117755145?ops_request_misc=%257B%2522request%255Fid%2522%253A%25222c386d3154a09ca64db54a5fba2b0365%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=2c386d3154a09ca64db54a5fba2b0365&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-17-117755145-null-null.nonecase&utm_term=layui%E4%B8%AD%E7%9A%84%E5%BC%B9%E7%AA%97%E5%9D%91&spm=1018.2226.3001.4450)

```

//弹窗3（js代码写在弹窗2中）
 
function configuration(){
    parent.layer.open({//占坑！
        type: 2,
        title: "配置项目",
        content: "/xx/xx/xx/xx?budgetMainCode="+budgetMainCode,
        area: ["80%", "80%"],
        end: function () {//点睛之笔，此端代码便是精髓之处，layui监听到弹窗3的销毁之后回调了一个end函数，通过这个end函数我们就能刷新弹窗2的数据
            refreshTable()//就比如这refreshTable()是弹窗2里面的用于拼接数据列表的函数
} }); }

```



## 实际项目中常用的弹窗和页面间的交互方法



### 1.layer open

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

### 2.1  弹窗关闭

```
2.1 	

function fn(){
	var index = parent.layer.getFrameIndex(window.name); //先得到当前iframe层的索引
	console.log(index)
	parent.layer.close(index); //再执行关闭  	
		}
```



### 2.禁用事件




```html
 <div class="add_icton_aniu" style="pointer-events: none;">  禁用事件
```

### 3. layui关闭当前弹窗   并刷新父页面

```
 var index = parent.layer.getFrameIndex(window.name);
                    parent.layer.close(index);
                    
 parent.window.$("iframe").attr("src",'page/mhgl/ksh_wdgl.html')
 
 
 parent.location.href='zhibiaofabu.html?YMID='+ ymid +'&YMMC='+ ymmc +'&BJZT=1';  //重定向 有刷新功能
```



### 4.操作父元素的dom

```
parent.window.$('.layui-layer-title').css({'color':'black'})
```

### 5.循环获取attr 属性值

```
$('input[name=' + key + ']').attr("value", map[key]);
```

### 6.改变父页面的locatin href地址

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

### 7.父页面刷新/当前的页面刷新

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

### 8.模仿自适应 

```
  $(".wrap").css("height", $(window).height());//模仿自适应  
    var aaa = ($(window).height() - $(".bg").height()) / 2;
    $(".bg").css("top", aaa);

```

### 9.eval() 函数 字符串计算

```
4.eval() 函数
  eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码。
 语法   eval(string)
```

### 10 layer.open title 样式

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

















