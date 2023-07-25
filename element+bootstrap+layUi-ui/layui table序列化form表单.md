# 1. layui table  serializeObject（）序列化数据提交

```html
		html部分
<form class="layui-form" lay-filter="iot" id="form-user-add">
			<input type="hidden" name="ID" id="PAGE_ID" value="" />
			<div class="layui-form-item">
				<label class="layui-form-label"><span class="layout-font-red">*</span> 页面名称：</label>
				<div class="layui-input-block">
					<input type="text" name="YMMC" placeholder="请输入" autocomplete="off" lay-verify="required" class="layui-input">
				</div>
			</div>
			<div class="layui-form-item">
				<label class="layui-form-label"> <span class="layout-font-red">*</span>页面顺序：</label>
				<div class="layui-input-block">
					<input type="text" name="YMSX" placeholder="请输入" autocomplete="off" lay-verify="required" class="layui-input">
				</div>
			</div>
			<div class="layui-form-item layout-submit-block btnboxout">
				<button class="layui-btn layui-bg-blue btnbox" lay-submit="" lay-filter="demo1">提交</button>
			</div>
		</form>
```
> ```js
> 
> 
> js部分
> 
> form.on('submit(demo1)', function (data) {
>     
>             var formData = $('#form-user-add').serializeObject();//作用是：将table id下
>     //所有的input name值，进行序列化可以向后台传输。
>     
>              console.log(formData)
>             if(ID){
>                sendData = $.extend({},formData,{ID:ID});
>             }else {
>                 sendData = $.extend({},formData,{CJR:userid});
>             }
>             sendAjax('DvKshdpYm/save', sendData, function (res) {
>                 if (res.success) {
>                     layer.msg(res.message);
>                     var index = parent.layer.getFrameIndex(window.name);
>                     parent.layer.close(index);
>                 	parent.window.$("iframe").attr("src",'page/mhgl/ksh_wdgl.html')
>                 }else{
>                 	layer.msg(res.message);
>                 }
>             }, null)
>             return false;
>         });
> ```

# JQuery的serializeObject 序列化form表单



```
/**
 * 使用场景：ajax提交表单数据
 */
/*
<form>
    <input type="text" name="username" value="123"/>
    <input type="text" name="password"  valur="abc"/>
 </form>
 */
 // 1. serialize() —— 序列化form表单 带name属性的内容为字符串
    JQuery("form").serialize();  
    // "username="123&password="abc"
	
// 2. serializeArray() ——返回JSON 对象数组
    JQuery("form").serializeArray();
    // [{name:"username",value:"123"},{name:"password",value:"abc"}]
 
//  3. 封装一个方法： serializeObject()  ——返回对象
	JQuery("form").serializeObject()
	//{username:"123",passwoed:"123"}
	
    JQuery.prototype.serializeObject = function () {
        var a,o,h,i,e;
        a = this.serializeArray();
        o={};
        h=o.hasOwnProperty;
        for(i=0;i<a.length;i++){
            e=a[i];
            if(!h.call(o,e.name)){
                o[e.name]=e.value;
            }
        }
        return o;
    }
```



