```
# 与天奋斗，其乐无穷！与地奋斗，其乐无穷！与人奋斗，其乐无穷！

 ———— 《毛泽东选集》之《奋斗自勉》（毛泽东1917年）
常用快捷键
加粗： Ctrl/Cmd + B
标题： Ctrl/Cmd + H
插入链接： Ctrl/Cmd + K
插入代码： Ctrl/Cmd + Shift + C
行内代码： Ctrl/Cmd + Shift + K
插入图片： Ctrl/Cmd + Shift + I
无序列表： Ctrl/Cmd + Shift + L
撤销： Ctrl/Cmd + Z
一级标题：快捷键为Crtl + 1，以此类推
————————————————
版权声明：本文为CSDN博主「千与千寻之前」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/cpongo3/article/details/88815697
```





# 1.正则匹配  字符串replace() 

```js
html = html.replace(/#{class}/g, "disable");



  html = html.replace(/#{active}/g, "active");
对目标字符串所有的#active  替换成active

replace() 方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。
```

# 2.定时刷新

 setTimeout("window.location.reload()", 1000);

# 3.控制父页面dom元素

# 4.jq css样式

```
parent.window.$("#main-body").attr("src",dUrl);  //表示  控制父页面dom元素  修改sr属性

parent.window.$('.layout-nav').css('text-align','left');
多个写法
$('#abc').css({
    fontSize : '12px',
    webkitBorderRadius : '5px',
    color : '#c00'
})

$('i').css("color","red")
```

# 5. 焦点事件

```
获取焦点事件
$("input").focus(function(){
    $("span").css("display","inline").fadeOut(4000);   //常用于输入框  获取焦点后显示DOM  4秒后消失
  });
失去焦点事件
$('input').focus(function(){
	$('i').css("display","block")
})
$('input').blur(function(){
	$('i').css("display","none")
})
```



# 6 获取dom属性

```
 设置属性 .setAttribute("属性","值")
获取属性 .getAttribute("属性")


原生获取

var ele = document.getElementById("dom");　
			var _width = window.getComputedStyle(ele).left;
			console.log(_width)


​				
​	var ele = document.getElementById("dom");　
​					var nowwidth = window.getComputedStyle(ele).left;
​					console.log(nowwidth)
​					if(nowwidth=='0px'){
​						nowwidth='200px'
​					}else{
​						nowwidth='0px'
​					}
​					$('main').animate({'left':nowwidth })


```

# 7 用到的jq 方法

```
$('.kshgl_list .list').remove();
$('.kshgl_list').append(html);
$('#tbck-nav').animate({'left':'-187px'});
var erji = $(this).children("a").children("i");


window.location.href = "../systemControl/qxgl.html";

```

# 8.//遍历赋值 将两个json对象合并为一个

```
function extend(o,n){
	for(var p in n){
		if(o[p] == undefined && n[p]!=undefined){
			o[p] = n[p];
		}
	}
	return o;
}
```

# 9.常规字符拼接

```
	$.ajax({
		type:"get",
		url:"json/world_link.json",
		async:true,
		success:function(data){
			console.log(data)
			var data=data.data;
		var str = '';
            for (let i in data) {
            	console.log(i)
                str+='<tr>\n' +
                    '<td>'+data[i].city+'</td>\n' +
                    '<td>'+data[i].sign+'</td>\n' +
                    '</tr>'
            }
            
            		$('#htmldom').html(str)
			console.log(str)	
	}
});
            //n'  字符串中是换行的标识符 第二行都是编程的时候需要写转义字符才能出现

浏览器打印时：效果
<tr>
<td>城市-0</td><td>签名-0</td>
</tr><tr>
<td>城市-1</td><td>签名-1</td>
</tr>
```

# 9.1  内容填充

```
  
  $('.kshgl_list_my div').remove();
   
		$('.kshgl_list_my').append(html);
```



# 10 es6拼接



```
var str = '';
            for (let i in data) {
                str+=`<tr>\n' +
                    <td>${data[i].id}</td>
                    <td>${data[i].name}</td>
                    <td>${data[i].team}</td>
                    <td>${data[i].password}</td>
                    </tr>`
            }
            //两种方法结果都是一样的
            
 注意事项：
 			var str = '';
            for (let i in data) {
                str+=`<tr>\n' +
                    <td>${data[i].city}</td>
                    <td>${data[i].sign}</td>                 
                    </tr>`
            }
            
         str+=`\n<p>我是后续添加</p>`;
           console.log(typeof(str))
         console.log(str)
         	$('#htmldom').html(str)
			成对匹配的标签  +其他标签   渲染时自动忽略    解决：换标签
      <tr>
' +
                    <td>城市-0</td>
                    <td>签名-0</td>                 
                    </tr><tr>
' +
                    <td>城市-1</td>
                    <td>签名-1</td>                 
                    </tr>
<p>我是后续添加</p>      

```

# 11  页面传值

```


function GetQueryString(name) {
    var reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)', 'i');
    var r = window.location.search.substr(1).match(reg);
    if (r != null) {
        return decodeURI(r[2]);
    }
    return null;
}
url?id= arr要传的值
使用
var id = GetQueryString("id");

第二种
function getUrlParams(){
    var paramsString = window.location.search.substr(1);
    var paramsArr = paramsString.split('&');
    var obj = {};
    paramsArr = $.each(paramsArr,function(i,e){
        var param = e.split('=');
        obj[param[0]] = param[1];
    });
    return obj;
}




```

# 12 * 判断字符为空

```
function isEmpty(obj) {
    if (obj === null) return true;
    if (typeof obj === 'undefined') {
        return true;
    }
    if (typeof obj === 'string') {
        if (obj === "") {
            return true;
        }
        if (obj.replace(/(^\s*)|(\s*$)/g, "").length == 0) return true;

        var reg = new RegExp("^([ ]+)|([　]+)$");
        return reg.test(obj);
    }
    return false;
}
```

# 13//数组为空

```
function arrEmpty(arr){
	for(var i=0;i<arr.length;i++){
		arr.splice(i,1);
		i = i-1;
	}
}
```

# 14 动态添加 css标签

```
document.write('<link rel="stylesheet" type="text/css" href="11.css"/>');
document.write('<script src="../../js/common.js" type="text/javascript" charset="utf-8"></script>');
```

# 15ewPlugins.min.js  JS网页背景颜色选择器插件

# 16  更换数组键名

```
var seriesData = []
data.value.forEach(function(item, index) {
    seriesData.push({
        value: item,
        name: data.legend[index]
    })
})
```



# 17empty()

```
$("#tabSwiper").empty();  //节点内清空 不清空 挂载点
```



# 18 jQuery.trim()方法

```
$.trim() 函数用于去除字符串两端的空白字符。
注意：$.trim()函数会移除字符串开始和末尾处的所有换行符，空格(包括连续的空格)和制表符。如果这些空白字符在字符串中间时，它们将被保留，不会被移除。
$(function () { 
    var str = "         lots of spaces before and after         ";
    $( "#original" ).html( "Original String: '" + str + "'" );
    $( "#trimmed" ).html( "$.trim()'ed: '" + $.trim(str) + "'" );
})
```

# 19 easyui

```
easyui是一种基于jQuery、Angular.、Vue和React的用户界面插件集合。
```

# 20 浏览器窗口大小改变时 执行方法

```
   $(window).resize(function() {
				selectWidth();
				selectTop();
			});
```

# 21 查询条件下拉框宽度

```
			function selectWidth() {
				$('#selectType').css('width', eval($('#selectTypeCheck').map(function() {
					return this.offsetWidth
				}).get().join('+')) + 'px');
				
			}
```

# 22 判断的经典用法

```
	$(function(){
				loadTb();
				$('#sliderToggle').click(function(){
					if($('#tbck-nav').hasClass('active')){
						//展开
						$('#tbck-nav').removeClass('active');
						$('#tbck-nav').animate({'left':'0px'});
						$('#main').animate({'left':'187px'});
						$('#sliderToggle').animate({'left':'177px'});
					}else{
						////收缩
						$('#tbck-nav').addClass('active');
						$('#tbck-nav').animate({'left':'-187px'});
						$('#main').animate({'left':'0px'});
						$('#sliderToggle').animate({'left':'0px'});
					}
				})
			})

```

23   封装请求

```
//$.ajax
function sendAjax(url, data, success, errors) {
    var layerLoading = null;
    var json = {"DEPTID":deptId,"USERID":userid};
    //判断是否有传递参数
    if(typeof(data) == 'object'){
    	//有参数，合并两个json字符串
    	data  = extend(json,data);
    	//console.log(data)
    }else{
    	//没有参数，直接传json参数
    	data = json;
    }
    
    $.ajax({
        type: 'POST',
        url: serverUrl + url,
        //async: false,
        data: data,
        dataType: 'json',
        beforeSend: function (XHR) {
            //发送ajax请求之前向http的head里面加入验证信息
            XHR.setRequestHeader("x-requested-key", "ZXWL " + ticket);
            layerLoading = layer.load(1, {
                shade: [0.1,'#fff']
            })
        },
        success: function (res) {
        	if(res.code == '500'){
        		var path = window.document.location.pathname;
        		var fileName = path.substring(0,path.substr(1).indexOf("/")+1);
        		top.location.href =window.location.protocol+"//"+window.location.host+fileName+"/404.html";
        	}
            layer.close(layerLoading);
            success(res);
        },
        error: function (XMLHttpRequest, textStatus, errorThrown) {
            checkLoginCookie();
        },
    });
}
```

# 23   //退出

```
function loginOut(){
	layer.confirm("您确定要退出吗？", {icon: 3, title:'提示'}, function(index){
		delCookie("dataInfo");
		sessionStorage.clear();
		window.document.location.href = "../../login.html";
        layer.close(index);
    }, function(index){
     	layer.close(index);
    });
    
}
```

# 24 属性选择器  及其他

   

```
  .top_title > a[href='tbgl-yfb.html']{color: white;}待处理
  
  
  3.选择器的使用
var biaogeTitle = $(this).parent('li').children('.biaoge-text').text();

var wd = $("li[data-wdid].zb-child-item.active");

var selector = $('#jscEcharts .top-lists').not('.list');
```

# 25  监听滚轮

```

$(document).ready(function(){
            var p=0;t=0;
            $(window).scroll(function(e){
                p=$(this).scrollTop();
                if(t<=p){
                    console.log('下滚')
                }
                else{
                    console.log('上滚')
                }
                t = p;
            })
        })
```

# 26 关于jq的事件对象

```
$("button").click(function(event) {
 console.log(event); // "click"事件
});

DOM事件对象得属性和方法
event对象包含与创建它的特定事件有关的属性和方法。触发的事件类型不一样，可用的属性和方法也不一样。不过所有事件都会包括下表列出的成员：
属性/方法	 类型	读/写     	 说明
 bubbles	 布尔	只读	 表明事件是否冒泡
 cancelable	 布尔	只读	 表明是否可以取消事件的默认行为
 currentTarget	 元素	只读	 其事件处理程序当前正在处理事件的那个元素
 detail	 整型	只读	 与事件相关的细节信息
 eventPhase	 整型	只读	 调节事件处理程序的阶段：1.表示捕获阶段 2.表示"处于目标" 3.表示冒泡阶段
 preventDefault()	 函数	只读	 取消事件的默认行为。如果cancelable是true，则可以使用这个方法
 stopPropagation	 函数	只读	 取消事件的进一步捕获或冒泡。如果bubbles为true，则可以使用这个方法
 target	 元素	只读	 事件的目标
 type	 字符串	只读	 被触发的事件的类型
 view	 AbstractView	只读	 与事件关联的抽象视图。等同于发生事件的window对象
————————————————
版权声明：本文为CSDN博主「人生无绝境」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qqj3066574300/article/details/80494554
```

# 27  trigger() 方法 指定事件

```
	
			$("input").select(function() {  //input 选中事件
				$("input").after("文本被选中！");  //选中事件执行的方法
			});
			var e = jQuery.Event("select");
			console.log(jQuery.Event("click"))//jq 封装的事件集
			
			$("button").click(function() {       //点击其他按钮，触发input的 select 事件
				$("input").trigger(e);
			});
		
			$("button").click(function(event) {
			 console.log(event); // "click"事件
			});
			
			项目使用
			
			 //监听select下拉选中事件
					form.on('select(type)', function(data) {
						var elem = data.elem; //得到select原始DOM对象
						$(elem).prev("a[lay-event='type']").trigger("click");
			});
```

