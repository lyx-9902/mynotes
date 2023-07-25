# bootstrap

参考

https://blog.csdn.net/u013938465/article/details/53507109

## 为什么使用 Bootstrap？

移动设备优先：自 Bootstrap 3 起，框架包含了贯穿于整个库的移动设备优先的样式。
浏览器支持：所有的主流浏览器都支持 Bootstrap。

容易上手：只要您具备 HTML 和 CSS 的基础知识，您就可以开始学习 Bootstrap。
响应式设计：Bootstrap 的响应式 CSS 能够自适应于台式机、平板电脑和手机。

- 它为开发人员创建接口提供了一个简洁统一的解决方案。

- 它包含了功能强大的内置组件，易于定制。

- 它还提供了基于 Web 的定制。

- 它是开源的。

  Bootstrap 包的内容
  基本结构：Bootstrap 提供了一个带有网格系统、链接样式、背景的基本结构。这将在 Bootstrap 基本结构 部分详细讲解。
  CSS：Bootstrap 自带以下特性：全局的 CSS 设置、定义基本的 HTML 元素样式、可扩展的 class，以及一个先进的网格系统。这将在 Bootstrap CSS 部分详细讲解。
  组件：Bootstrap 包含了十几个可重用的组件，用于创建图像、下拉菜单、导航、警告框、弹出框等等。这将在 布局组件 部分详细讲解。
  JavaScript 插件：Bootstrap 包含了十几个自定义的 jQuery 插件。您可以直接包含所有的插件，也可以逐个包含这些插件。这将在 Bootstrap 插件 部分详细讲解。
  定制：您可以定制 Bootstrap 的组件、LESS 变量和 jQuery 插件来得到您自己的版本。

  

## Bootstrap支持的js插件

Bootstrap的JavaScript插件可以单独导入到页面中，也可以一次性导入到页面中。

一次性导入：

Bootstrap提供了一个单一的文件，这个文件包含了Bootstrap的所有JavaScript插件，即bootstrap.js（压缩版本：bootstrap.min.js）。

单独导入：

为方便单独导入特效文件，Bootstrap V3.2中提供了12种JavaScript插件，他们分别是：

☑ 动画过渡（Transitions）:对应的插件文件“transition.js”

☑ 模态弹窗（Modal）:对应的插件文件“modal.js”

☑ 下拉菜单（Dropdown）：对应的插件文件“dropdown.js”

☑ 滚动侦测（Scrollspy）：对应的插件文件“scrollspy.js”

☑ 选项卡（Tab）：对应的插件文件“tab.js”

☑ 提示框（Tooltips）：对应的插件文件“tooltop.js”

☑ 弹出框（Popover）：对应的插件文件“popover.js”

☑ 警告框（Alert）：对应的插件文件“alert.js”

☑ 按钮（Buttons）：对应的插件文件“button.js”

☑ 折叠/手风琴（Collapse）：对应的插件文件“collapse.js”

☑ 图片轮播Carousel：对应的插件文件“carousel.js”

☑ 自动定位浮标Affix：对应的插件文件“affix.js”

上述单独插件的下载可到github去下载（https://github.com/twbs/bootstrap）。




#  快速入门

引入js css   jquery

```
<!doctype html>
<html lang="zh-CN">
  <head>
    <!-- 必须的 meta 标签 -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap 的 CSS 文件 -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- JavaScript 文件是可选的。从以下两种建议中选择一个即可！ -->

    <div class="alert alert-primary" role="alert">
        A simple primary alert—check it out!
      </div>


      <div class="alert alert-primary" role="alert">
        A simple primary alert with <a href="#" class="alert-link">an example link</a>. Give it a click if you like.
      </div>


    <!-- 选项 1：jQuery 和 Bootstrap 集成包（集成了 Popper） -->
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-LCPyFKQyML7mqtS+4XytolfqyqSlcbB3bvDuH9vX2sdQMxRonb/M3b9EmhCNNNrV" crossorigin="anonymous"></script>

    <!-- 选项 2：Popper 和 Bootstrap 的 JS 插件各自独立 -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.min.js" integrity="sha384-gRC4eoaRyQ8xv2X6Mnf+eOIrtON3wId3dAkwO0HQX26OrFBoLpjX/XWOJacSiZhL" crossorigin="anonymous"></script>
    -->
  </body>
</html>
```

# 踩坑：

```


<script src="./js/bootstrap.bundle.js"></script>   全部模块 js 功能测试失败的原因是，引入的js不是全部。

```



# attr

 $('#sel').attr("id", "uasUserRole1111")

```
id="uasUserRole1111"     标签赋值添加id  class
```

# if的简写



```
“” 为false  "00" 为true

if("0") alert(0)
```



# Buttons

关键点： type="button" 属性，以便js识别，初始化； class="btn btn-primary"  按钮基本css, 和颜色css.

```
<button type="button" class="btn btn-primary">Primary</button>
```

其他颜色：

```html
primary
secondary
success
danger
warning
info
light
dark
link
```



# 1. Forms

```
 <form>

        <div class="form-group">
            
          <label for="exampleFormControlInput1">Email address</label>
          <input type="email" class="form-control" id="exampleFormControlInput1"                      placeholder="name@example.com">
        </div>

      </form>
```

# 2.警告框（Alert）

```
<div class="alert alert-primary" role="alert">
  A simple primary alert—check it out!
</div>
```

# 3.模态框（弹窗）DOM 部分

关键点：  data-target="#exampleModal"

id="exampleModal" 对应 id

```javascript

<!-- Button trigger modal -->
    
    
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
    点击弹窗
  </button>
  
  <!-- Modal -->
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    
    <div class="modal-dialog">

      <div class="modal-content">

        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>


        <div class="modal-body">
          ...
        </div>


        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>

      </div>

    </div>

  </div>
  
```

### 弹窗的弹出

在不使用js情况下弹出来

```javascript
属性： data-toggle="modal" data-target="#exampleModal"  指定弹窗属性和弹窗对象。

<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
    点击弹窗
  </button>
  
```

### 使用js

```
$('#identifier').modal(options)
打开
$('#identifier').modal('show')

eg:  点击按钮，打开弹窗
$('#modal').click(function () {

            $('#exampleModal').modal('show')
        })

```

### 关闭

```
$('#identifier').modal('hide')
```

### 弹窗的回调函数   即钩子函数

事件类型	描述
show.bs.modal	show 方法调用之后立即触发该事件。如果是通过点击某个作为触发器的元素，则此元素可以通过事件的 relatedTarget 属性进行访问。
shown.bs.modal	此事件在模态框已经显示出来（并且同时在 CSS 过渡效果完成）之后被触发。如果是通过点击某个作为触发器的元素，则此元素可以通过事件的 relatedTarget 属性进行访问。
hide.bs.modal	hide 方法调用之后立即触发该事件。
hidden.bs.modal	此事件在模态框被隐藏（并且同时在 CSS 过渡效果完成）之后被触发。
loaded.bs.modal	从远端的数据源加载完数据之后触发该事件。

```
$('#modal').click(function () {

            $('#exampleModal').modal('show')
        })
```

案例： 需求， 弹窗打开前的回调

```
 $('#modal').click(function () {

            $('#exampleModal').modal('show')
        })
        $('#exampleModal').on('show.bs.modal', function (event) {
            // do something... 
            alert("我是show钩子")
        })
```

# 4 Toast  （未测试成功）

## 定义和使用

**Toast** 组件就像一个警报框，仅在发生某些情况（即用户单击按钮，提交表单等）时显示几秒钟。



# 5. Bootstrap-select  单独（组件）

https://www.bootstrapselect.cn/
既然是bootstrap-select，组件肯定是依赖bootstrap的，而bootstrap又是依赖jquery的，所以使用组件必须引用如下文件。

### 1 使用js css 配置

```
<link href="Content/bootstrap/css/bootstrap.min.css" rel="stylesheet" />
<link href="Content/bootstrap-select/css/bootstrap-select.min.css" rel="stylesheet" />

<script src="Content/jquery-1.9.1.min.js"></script>
<script src="Content/bootstrap/js/bootstrap.min.js"></script>
<script src="Content/bootstrap-select/js/bootstrap-select.min.js"></script>
<script src="Content/bootstrap-select/js/i18n/defaults-zh_CN.min.js"></script>

或者是下面这样

<link rel="stylesheet"
        href="https://cdn.jsdelivr.net/npm/bootstrap-select@1.13.9/dist/css/bootstrap-select.min.css">

 <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js"
        integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous">
    </script>
```

### 2 DOM 部分

```
1.使用就更加简单了，不用任何已经js，直接使用class就可以初始化。
<select class="selectpicker">
    <option value="1">广东省</option>
    <option value="2">广西省</option>
    <option value="3">福建省</option>
    <option value="4">湖南省</option>
    <option value="5">山东省</option>                            
</select>
```

### 其他属性

```

2. multiple 属性，自动可以多选

  <select class="selectpicker" multiple>
        <option value="1">广东省</option>
        <option value="2">广西省</option>
        <option value="3">福建省</option>
        <option value="4">湖南省</option>
        <option value="5">山东省</option>
    </select>
3. data-live-search="true"  自动可以 检索功能
   <select class="selectpicker" multiple  data-live-search="true">
        <option value="1">广东省</option>
        <option value="2">广西省</option>
    </select>
    4. optgroup 标签，实现下拉分组
     <select class="selectpicker" multiple  data-live-search="true">
        <optgroup label="广东省">
            <option value="1">广州市</option>
            <option value="2">深圳市</option>
            <option value="3">珠海市</option>
     </optgroup> 


    </select>
 5. data-max-options="2"   限选2个
 <select class="selectpicker" multiple data-live-search="true" data-max-options="2">
    <option value="1">广东省</option>
    <option value="2">广西省</option>
    <option value="3">福建省</option>
    <option value="4">湖南省</option>
    <option value="5">山东省</option>                            
</select>
6. 缩略模式，比如当选中值大于3个的时候只显示选中项的个数，注意这个属性只对多选生效
data-selected-text-format="count > 3"

7.显示带颜色的标签
<select class="form-control selectpicker" title="请选择省份" multiple>
                        <option data-content="<span class='label label-success'>广东省</span>">广东省</option>    
                        <option data-content="<span class='label label-info'>广西省</span>">广西省</option>                         
</select>
```



### js 组件取值赋值

#### a  组件取值

```
关于组件取值保持原生的jquery方法，比如 var value = $('#sel').val(); 这样是不是很简单，需要注意的是，如果是多选，这里得到的value变量是一个数组变量，形如 ['1','2','3']。
```

#### b 组件赋值

```
组件赋值就需要稍微变换一下了，正确的赋值方法为：
$('.selectpicker').selectpicker('val', '1');
```

在一些级联选择的使用场景中，经常需要在赋值的时候顺便触发一下组件的change事件，我们可以这么做。

```
$('.selectpicker').selectpicker('val', '1').trigger("change");
```

如果是多选的赋值，也是一样

```
$('.selectpicker').selectpicker('val', ['1','2','3']).trigger("change");
```

3.

全选： $('.selectpicker').selectpicker('selectAll');    测试无效

反选： $('.selectpicker').selectpicker('deselectAll'); 测试无效

4.

组件禁用：

```
$('.disable-example').prop('disabled', true);
$('.disable-example').selectpicker('refresh');  测试无效
```

组件启用：

```
$('.disable-example').prop('disabled', false);
```

组件销毁：

```
$('.selectpicker').selectpicker('destroy');   变为普通
```

####  3 . Bootstrap-select  动态渲染

```
见 角色管理页面

                    var $select = document.createElement("select");
                    $($select).addClass("selectpicker show-menu-arrow form-control").attr("multiple", true);
                    $("#multiple_user_role").empty().append($select);

                    $("#multiple_user_role select").attr("id", "uasUserRole").attr("name", "uasUserRole").attr("data-size", "10");

                    $("#uasUserRole").insertOptionByOther(res.resultData, "roleCode", "roleName", "");
               
                    $("#uasUserRole").selectpicker('refresh');

                    $("#uasUserRole").selectpicker('val', role);
```

### 下拉选择组件使用总结： 

 使用流程包含： dom  js赋值，取值， 如果是动态的，包含option 原始dom替换，bootstrap.js重新渲染，需要使用selectpicker方法重新渲染。

# 4 bootstrapValidator 表单验证 组件

```
 $("#action_form").bootstrapValidator({
                    message: 'This value is not valid',
                    excluded: [':disabled']

                });
```





# 5 弹出框（Popover）插件

弹出框（Popover）与工具提示（Tooltip）类似，只需把鼠标悬停在元素上即可。

弹出框（Popover）插件不像之前所讨论的下拉菜单及其他插件那样，它不是纯 CSS 插件。如需使用该插件，您必须使用 jquery 激活它（读取 javascript）。

使用方法：

点击出现： 准备DOM， js加载初始方法；

如果是hover触发，直接准备dom就好。如果在加载js，会覆盖hover效果。

### 触发方式：

####  dada属性出发：

加两个属性实现。

```
<a href="#" data-toggle="popover" title="Example popover">
    请悬停在我的上面
</a>
```

单独dom，实现hover触发

   指定dom点击触发： $('#test').popover()

**通过 JavaScript：**通过 JavaScript 启用弹出框（popover）：

```
$('#identifier').popover(options)
```

启用页面中的所有的弹出框（popover）

```
$(function () { $("[data-toggle='popover']").popover(); });
```

其他属性：

复杂结构属性组成：

```
 <button type="button" class="btn btn-success" 
 
 id="bottom"
 title="Popover title"    标题 
 data-container="body"    正文
 data-toggle="popover"     标记：弹窗tips
 data-placement="bottom"    弹出位置：下侧
data-content="底部的 Popover 中的一些内容"   弹出的内容
data-animation="true"     向弹出框应用 CSS 褪色过渡效果。
data-trigger="click"  触发方式  定义如何触发弹出框： click| hover | focus | manual。。
>
底部的 Popover
 </button>
```

API方法

```
1.  $().popover(options)  向元素集合附加弹出框句柄
```

```
2. $('#element').popover('toggle')  切换显示/隐藏元素的弹出框。
```

```
3. $('#element').popover('hide')隐藏元素的弹出框
```

```
4. $('#element').popover('destroy') 隐藏并销毁元素的弹出框
```

```
5.$('#element').popover('show')显示
```





# 6 Dropdowns

DOM

```
   <div class="btn-group dropleft">
        <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown button
        </button>
        <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
          <a class="dropdown-item active" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </div>
```

.dropup   class 控制打开方向 

class="dropdown-item active"  默认选中

其他方法和属性，类似于弹窗。

$().dropdown('toggle')



# 7 Tooltips

DOM

```
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="top" title="Tooltip on top">
  Tooltip on top
</button>
```

和弹窗类似

# 8 Spinners（loading...）

DOM

关键dom是外层的。

```
  <div class="spinner-border" role="status">
      <span class="sr-only">Loading...</span>
    </div>
```

和按钮组合使用

```
 <button class="btn btn-primary" type="button" disabled>
    <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
    Loading...
  </button>
```



# 9 table  表格

表单： 在bootstrap中，作为一个单独的js插件。

Bootstrap Table插件通过数据属性或JavaScript以表格格式显示数据。

https://www.bootstrap-table.com.cn/doc/getting-started/usage/ 文档

https://bootstrap-table.com/docs/getting-started/introduction/     文档

https://bootstrap-table.com/

```
# bootstrap-table-examples

[Bootstrap Table Docs](https://bootstrap-table.com/)

[Bootstrap Table Examples](https://examples.bootstrap-table.com)

[jsFiddle Examples](https://github.com/wenzhixin/bootstrap-table-examples/blob/master/jsfiddle_examples.md)

[CRUD Example](https://github.com/wenzhixin/bootstrap-table-examples/blob/master/crud/README.md)

## reporting issues

All issues need to be submitted to the main project, not this examples repo.

Please read: [CONTRIBUTING.md#bug-reports](https://github.com/wenzhixin/bootstrap-table/blob/develop/CONTRIBUTING.md#bug-reports) and post issue to [issue](https://github.com/wenzhixin/bootstrap-table/issues), thanks!

```

使用方法:

1  依赖的 css  js。

2  DOM

通过数据属性

```html
  <table data-toggle="table">
        <thead>
          <tr>
            <th>Item ID</th>
            <th>Item Name</th>
            <th>Item Price</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>Item 1</td>
            <td>$1</td>
          </tr>
        </tbody>
      </table>
```

我们还可以通过`data-url="data1.json"`在普通表上设置来使用远程URL数据。

```html
<table
  data-toggle="table"
  data-url="data1.json">
  <thead>
    <tr>
      <th data-field="id">Item ID</th>
      <th data-field="name">Item Name</th>
      <th data-field="price">Item Price</th>
    </tr>
  </thead>
</table>
```

您还可以添加`pagination`，`search`和`sorting`表格，如下表所示。

```html
<table
  data-toggle="table"
  data-url="data1.json"
  data-pagination="true"
  data-search="true">
  <thead>
    <tr>
      <th data-sortable="true" data-field="id">Item ID</th>
      <th data-field="name">Item Name</th>
      <th data-field="price">Item Price</th>
    </tr>
  </thead>
</table>
```

## 通过JavaScript

通过JavaScript调用带有id表的bootstrap Table。

```
<table id="table"></table>


$('#table').bootstrapTable({
  columns: [{
    field: 'id',
    title: 'Item ID'
  }, {
    field: 'name',
    title: 'Item Name'
  }, {
    field: 'price',
    title: 'Item Price'
  }],
  data: [{           - ---- 通过data传入数据
    id: 1,
    name: 'Item 1',
    price: '$1'
  }, {
    id: 2,
    name: 'Item 2',
    price: '$2'
  }]
})



```

$('#table').bootstrapTable( {option })可以使用的参数有哪些

项目案例：

第一个主要参数：columns 

一下是columns内的属性

```
1 复选框
 columns：[{  checkbox: "true"}]    设置`true`为显示一个复选框。复选框列具有固定的宽度。
 radio  单选框
2.  单元格的对齐方式
  <th data-field="name" data-halign="center" data-align="left">Item Name</th>
3 cellStyle   单元格的样式  
   Function
            单元格样式格式化程序功能，采用四个参数：

            value：字段值。
            row：行记录数据。
            index：行索引。
            field：行字段。
            支持类或CSS。
4  columns：[ class: 'success',]    为每一行固定添加class
5 Click To Select  效果是：在你点击某一列或某一个单元格时，复选框选中。
 columns：[  clickToSelect:true,]     测试，放到一级属性也是可以的。

6 Rowspan Colspan  单元格合并
7 detailFormatter 
  使用方式： formatter  : function (value, row, index){  return value + "修改项"; } 对单元格显示数据格式化
8   visible: false,   列隐藏和显示。 可以用于自定义显示用户想看到的列。
9   data-search="true"   data-searchable="false"  table 和 col 两个属性配合使用，用于检索。
10 responseHandler 
       responseHandler: function (res) {
    $("#invite_count").html(res.count);//count  后端返回的非total、rows数据
    $("#invite_month").html(res.month);
    return{                            //return bootstrap-table能处理的数据格式
        "total":res.total,
        "rows":res.rows
    }
   响应头数据格式化： 作用是，回调参数是请求返回的数据，进行格式化成table可以使用的格式。
  11  table  操作行，实现方法：
  {field: 'ACTION',title: '操作', width:"200", formatter:action}
  
  返回  字符串形式的按钮。  按钮中包含原生的点击事件。并使用回调参数。
   var buttonList = {
    delete : '&nbsp;<a data-toggle="tooltip" data-placement="left" title="删除" onclick="rm_page.del(\''+fd_id+'\')"><i class="glyphicon glyphicon-trash grid_action red_bgColor"></i></a>&nbsp;'
        };
    //表格操作
    action : function(value, row, index) {
        var fd_id = row.fdObjectid;
        var role_code = row.roleCode;
        return rm_page.gridButton(fd_id, role_code).join('');
    },  
```



```
  tableData : function(_url, _columns, singleSelect, hasSub) {
        var checkBoxColumn = [{field: 'state',checkbox: true}];//每行的checkbox
        load_grid_colomn.$tab.bootstrapTable('destroy');
        load_grid_colomn.$tab.bootstrapTable({
            method: 'POST',							//请求方式
            toolbar: '#toolbar', 					//工具按钮用哪个容器
            url: _url,
            contentType:"application/x-www-form-urlencoded; charset=UTF-8",			//发送到服务器的数据编码类型
            // contentType:"application/j1son;charset=utf-8",
            queryParams: load_grid_colomn.queryParams,		//传递参数
            queryParamsType:"limit",				//设置为 'limit' 则会发送符合 RESTFul 格式的参数.
            cache: true,							//是否使用缓存，默认为true，所以一般情况下需要设置一下这个属性
            striped: true,							//为 true 会有隔行变色效果
            pagination: true,						//分页
            pageSize: 10,							//页面数据条数
            pageNumber:1,							//首页页码
            pageList: [5,10, 25, 50, 100],			//设置可供选择的页面数据条数
            sidePagination:'server',				//设置为服务器端分页
            detailView:hasSub,						//父子表
            checkbox:true,
            singleSelect:singleSelect,              // 单选checkbox
            showColumns: true,
            clickToSelect: true,
            minimumCountColumns: 1,
            uniqueId: load_grid_colomn.uniqueColumn,
            searchParams: load_grid_colomn.queryData,
            synchronizedFun : load_grid_colomn.methods,//查询同步方法
            responseHandler: function responseHandler(res){
                if(res.code != 200) {
                    return {rows:[], total:0};
                };
                res = res.resultData;

                return {
                    rows:res.dataList,
                    "total": res.total
                };
            },
            columns:checkBoxColumn.concat(this.columns),
            formatLoadingMessage: function () {
                return "请稍等，正在加载中...";
            },
            formatNoMatches: function () {  //没有匹配的结果
                return '无符合条件的记录';
            },
            //表头
            columns : _columns,
            onLoadError: function(XMLHttpRequest){
                errorHandler(XMLHttpRequest);
            },
            onCheck:function(row){
            },
            onUncheck:function(row){
            },
            onLoadSuccess:function(data){

                $("#table_box").mCustomScrollbar("destroy");
                $("#table_box").mCustomScrollbar({theme:"menu-list"});

                $("body").initMyTooltip();
            },
            //$detail:当前行下面创建的新行里面的td对象
            onExpandRow: function(index, row, $detail){
                subTable.init(index, row, $detail);
            }
        });
```



项目使用：

```js
    //表格字段
    getTabCol : function(table_id){
        var params = {roleName:$("#roleName_query").val(), roleCode:$("#roleCode_query").val()};

        var gridParams = {url:"/api-auth/role/getRoleByPageAndCondition", queryParams:params,         //singleSelect:false,
                columns:[
                    {field: '', width:50, title: '序号', formatter:function(value, row, index){
                        var pageSize=$('#'+table_id).bootstrapTable('getOptions').pageSize;
                        var pageNumber=$('#'+table_id).bootstrapTable('getOptions').pageNumber;
                        return pageSize * (pageNumber - 1) + index + 1;
                    }},
                
                ]};
        var ta = $("body").data("table_action");
        if(JSON.stringify(ta) != "{}")
            gridParams.columns.push({field: 'ACTION',title: '操作', width:"200", formatter:rm_page.action});

        return gridParams;
    },
```

### 官方设置属性：

```
名称	标签	类型	默认	描述
radio	data-radio	Boolean	FALSE	设置为 True 在列前添加一个固定宽度的 单选按钮
checkbox	data-checkbox	Boolean	FALSE	设置为 True 在列前添加一个固定宽度的 复选框
field	data-field	String	undefined	列的名称
title	data-title	String	undefined	列的标题
titleTooltip	data-title-tooltip	String	undefined	列标题的提示文本，支持HTML 属性
class	class / data-class	String	undefined	设置列的 class 属性
rowspan	rowspan / data-rowspan	Number	undefined	设置一个单元格可以占多少行
colspan	colspan / data-colspan	Number	undefined	设置一个单元格可以占多少列
align	data-align	String	undefined	单元格中的数据水平方向的位置，'left', 'right', 'center'
halign	data-halign	String	undefined	列头中的数据水平方向的位置 ，'left', 'right', 'center'
falign	data-falign	String	undefined	列尾中的数据水平方向的位置 ，'left', 'right', 'center'
valign	data-valign	String	undefined	单元格中的数据垂直方向的位置， 'top', 'middle', 'bottom'
width	data-width	Number {Pixels or Percentage}	undefined	设置列的宽度，可以使用像素或百分比
sortable	data-sortable	Boolean	FALSE	设置为 True 允许对列进行排序
order	data-order	String	'asc'	默认的排序方式，'asc' or 'desc'.
visible	data-visible	Boolean	TRUE	Table模式设置为 False 会隐藏列的内容
cardVisible	data-card-visible	Boolean	TRUE	Card模式设置为 False 会隐藏列的内容
switchable	data-switchable	Boolean	TRUE	设置为 False 将禁止对列进行隐藏展示切换
clickToSelect	data-click-to-select	Boolean	TRUE	设置为 True 点击列的时候选中单选按钮或者复选框
formatter	data-formatter	Function	undefined	设置该列数据的格式
footerFormatter	data-footer-formatter	Function	undefined	设置该列列脚的数据格式
events	data-events	Object	undefined	设置单元格的事件监听器，包含4个参数
event：jquery事件
value：监听列的当前单元格的值
row：当前行完整内容
index：当前行的索引值
sorter	data-sorter	Function	undefined	自定义排序方法，包含两个参数
a：单元格A的数据
b：单元格B的数据
sortName	data-sort-name	String	undefined	自定义指定一个其他的列名，并通过这一列的值对当前列进行排序
cellStyle	data-cell-style	Function	undefined	指定单元格的样式，包含3个参数
value:列名称
row:行数据
index:行号
searchable	data-searchable	Boolean	TRUE	设置为 True 搜索时可以对本列的内容进行搜索
searchFormatter	data-search-formatter	Boolean	TRUE	设置为 True 使用格式化数据进行搜索
escape	data-escape	Boolean	FALSE	设置为 True 转义特殊字符
showSelectTitle	data-show-select-title	Boolean	FALSE	设置为 True  显示包含  'radio' 、'singleSelect' 'checkbox'选项的列
————————————————
版权声明：本文为CSDN博主「pengjunlee」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/pengjunlee/article/details/80658596
```



我们还可以通过设置来使用远程URL数据`url: 'data1.json'`。

```
$('#table').bootstrapTable({
  url: 'data1.json',
  columns: [{
    field: 'id',
    title: 'Item ID'
  }, {
    field: 'name',
    title: 'Item Name'
  }, {
    field: 'price',
    title: 'Item Price'
  }]
})
```

您还可以添加`pagination`，`search`和`sorting`表格，如下表所示。

```
$('#table').bootstrapTable({
  url: 'data1.json',
  pagination: true,
  search: true,
  columns: [{
    field: 'id',
    title: 'Item ID'
  }, {
    field: 'name',
    title: 'Item Name'
  }, {
    field: 'price',
    title: 'Item Price'
  }]
})
```



### 2  表格的样式调整

样式通过class添加

table  添加bootstrap 样式

table-striped    隔行变色

table-bordered  边框

table-hover   悬停

table-condensed 表格紧凑

<tr class="info">   状态色

  table 包裹一个div。  加上class="table-responsive"， 响应式状态。  表格内容较多时，自动滚动条。

```
    <table class="table table-striped">
        <thead>
            <tr>
                <th>Item ID</th>
                <th>Item Name</th>
                <th>Item Price</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>Item 1</td>
                <td>$1</td>
            </tr>
        </tbody>
    </table>
```







核实：

```
 var sbl = $("body").data("table_action");    //

(JSON.stringify(ta) != "{}")

 $("#action_form").bootstrapValidator("validate");

 tipsModal(code_msg["code_"+*res*.code], "noConfirm");
```

