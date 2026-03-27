# Layui组件使用

 心得总结： 组件执行出现异常时  》 layui官网在线测试网页上执行代码 》 如果正常了，则是js依赖的问题，重新下载依赖包。引入项目。



## 表单组件

<img src=".\img\11.png" style="zoom:75%;" />

   功能： js 赋值，和获取值，提交而不跳转页面。重置功能。

其要点为：

- 通过 `class="layui-form"` 定义一个表单域，通常设置在`<form>`标签上， 或普通`<div>` 标签亦可。
- 通过 `class="layui-form-item"` 定义一个块级元素的表单项容器
- 通过 `class="layui-form-label"` 定义标签
- 通过 `class="layui-input-block"` 定义表单项父容器为块级元素
- 通过 `class="layui-input-inline"` 或 `class="layui-inline"` 定义表单项父容器为行内块元素

即必须按照规定的层级定义相应的 `class`。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Layui行内表单</title>
  <link href="/lib/layui-v2.13.5/css/layui.css" rel="stylesheet">
</head>
<body>

<form class="layui-form" lay-filter="demo-form" style="margin:20px;">

  <!-- ======================
  重点：行内布局（并排显示）
  layui-inline + layui-input-inline
  ====================== -->
  <div class="layui-form-item">
    <!-- 外层：layui-inline = 让这一整块 行内显示 -->
    <div class="layui-inline">
      <label class="layui-form-label">姓名</label>
      <!-- 内层：layui-input-inline = 输入框行内显示 -->
      <div class="layui-input-inline">
        <input type="text" name="username" lay-verify="required" 
               placeholder="请输入" class="layui-input">
      </div>
    </div>

    <!-- 第二个表单项 自动跟在后面并排 -->
    <div class="layui-inline">
      <label class="layui-form-label">爱好</label>
      <div class="layui-input-inline">
        <select name="interest">
          <option value="">请选择</option>
          <option value="0">写作</option>
          <option value="1">阅读</option>
          <option value="2">游戏</option>
        </select>
      </div>
    </div>
  </div>

  <!-- 按钮 -->
  <div class="layui-form-item">
    <div class="layui-input-block">
      <button type="button" class="layui-btn" id="setVal">赋值</button>
      <button type="button" class="layui-btn" id="getVal">取值</button>
      <button type="reset" class="layui-btn layui-btn-primary">重置</button>
      <button type="submit" class="layui-btn layui-btn-normal" lay-submit>提交</button>
    </div>
  </div>

</form>

<script src="/lib/layui-v2.13.5/layui.js"></script>
<script>
layui.use(['form','layer'],function(){
  var form = layui.form;
  var layer = layui.layer;

  // 赋值
  document.getElementById('setVal').onclick = function(){
    form.val('demo-form', {
      username: "张三",
      interest: "1"
    });
  };

  // 取值
  document.getElementById('getVal').onclick = function(){
    var data = form.val('demo-form');
    layer.msg(JSON.stringify(data));
  };

  // 提交
  form.on('submit', function(data){
    layer.alert("提交："+ JSON.stringify(data.field));
    return false;
  });
});
</script>

</body>
</html>
```



###  按钮中的type

重置功能的前提是，按照规则的class, 在input  select 上加上name属性。

```
 <button type="reset" class="layui-btn layui-btn-primary">重置</button>
```

## API

| API                                                          | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| var form = layui.form                                        | 获得 `form` 模块。                                           |
| [form.render(type, filter)](https://layui.dev/docs/2/form/#render) | 表单域组件渲染，核心方法。[#用法](https://layui.dev/docs/2/form/#render) |
| [form.verify(obj)](https://layui.dev/docs/2/form/#verify)    | 自定义表单验证的规则。[#用法](https://layui.dev/docs/2/form/#verify) |
| [form.validate(elem)](https://layui.dev/docs/2/form/#validate) 2.7+ | 主动触发执行验证。[#用法](https://layui.dev/docs/2/form/#validate) |
| [form.val(filter, obj)](https://layui.dev/docs/2/form/#val)  | 表单赋值或取值。 [#用法](https://layui.dev/docs/2/form/#val) |
| [form.submit(filter, callback)](https://layui.dev/docs/2/form/#submit) 2.7+ | 用于主动执行指定表单的提交。[#用法](https://layui.dev/docs/2/form/#submit) |
| [form.on('event(filter)', callback)](https://layui.dev/docs/2/form/#on) | 事件。[#用法](https://layui.dev/docs/2/form/#on)             |
| [form.set(options)](https://layui.dev/docs/2/form/#set)      | 设置 form 组件全局配置项。                                   |
| form.config                                                  | 获取 form 组件全局配置项。                                   |

## 属性

在表单域中，有时还需要定义一些特定属性来配合组件的使用，它们一般以 `lay-*` 为命名格式，如：

```
<form class="layui-form" lay-filter="form-1">

  <input type="text" class="layui-input" lay-verify="email">

  <input type="checkbox" lay-skin="switch" lay-filter="agree" title="同意">

  <button class="layui-btn" lay-submit>提交</button>

</form>
```

以下为 `form` 组件的特定属性列表：

| 属性                               | 值                                                           | 描述                                                         |
| :--------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| title                              | 自定义                                                       | 设置表单元素标题，一般用于 `checkbox,radio` 元素             |
| lay-filter                         | 自定义                                                       | 设置表单元素的过滤器，以便用于执行相关方法时的参数匹配       |
| lay-verify                         | `required`必填项 `phone`手机号 `email`邮箱 `url`网址 `number`数字 `date`日期 `identity`身份证`自定义规则值` | 设置表单项的验证规则，支持单条或多条规则（多条用`|`分隔），如： `lay-verify="required"` `lay-verify="required|email"` `lay-verify="其他自定义规则值"`自定义规则的用法：[#详见](https://layui.dev/docs/2/form/#verify)注：2.8.3 版本中调整了内置规则，不再强制必填。 如需保留必填，可叠加 `required` 规则，如： `lay-verify="required|number"` |
| lay-vertype                        | `tips`吸附层 `alert` 对话框 `msg` 默认                       | 设置验证异常时的提示层模式                                   |
| lay-reqtext                        | 自定义                                                       | 设置*必填项*（`lay-verify="required"`）的默认提示文本        |
| lay-affix                          | [#详见](https://layui.dev/docs/2/form/input.html#affix)      | 输入框动态点缀，`<input type="text">`元素 **私有属性**       |
| lay-skin                           | [#详见](https://layui.dev/docs/2/form/checkbox.html#default) | 设置 UI 风格。 `<input type="checkbox">`，`<input type="radio">` 元素 **私有属性** |
| lay-search                         | 2.9.15+ `lay-search="{caseSensitive:false, fuzzy: false}"` `caseSensitive` 是否区分大小写，默认值为 `false` `fuzzy`是否开启模糊匹配，开启后将会忽略匹配字符出现在字符串中的位置，默认值为 `false` 设置`cs`区分大小写(2.9.15+ 已弃用) | 给 `select` 组件开启搜索功能。`<select>` 元素 **私有属性**   |
| lay-creatable 2.9.7+               | 无需值                                                       | 是否允许创建新条目，需要配合 `lay-search` 使用。`<select>` 元素 **私有属性** |
| lay-append-to 2.9.12+ 实验性       | `body`                                                       | 是否将 select 面板追加到 body 元素中。`<select>` 元素 **私有属性** |
| lay-append-position 2.9.12+ 实验性 | `absolute` 绝对定位 (默认) `fixed` 固定定位                  | 用于设置 select 面板开启 `lay-append-to` 属性后的定位方式。`<select>` 元素 **私有属性** |
| lay-submit                         | 无需值                                                       | 设置元素（一般为`<button>` 标签）触发 `submit` 提交事件      |
| lay-ignore                         | 无需值                                                       | 设置表单元素忽略渲染，即让元素保留系统原始 UI 风格。注 2.10.2+：该属性若设置在 `<div>` 等父元素上，则该父元素下的所有表单均可被忽略渲染。 |

## 表单的渲染

layui在常规form表单标签，加载完毕后，执行渲染方法，会对input美化；下拉select进行替换。

```
form.render(type, filter);
```

- 参数 `type` 可选，对应表单组件类型，支持：`input,select,checkbox,radio`；若不填，则指向所有类型。
- 参数 `filter` 可选，对应 `class="layui-form"` 所在元素的 `lay-filter` 属性值，用于指定需渲染的表单区域。

### **常规渲染**

`form` 组件会在元素加载完毕后，自动对所有表单区域完成一次渲染，因此该方法主要用于对*动态插入*的表单元素的渲染。

```html
<form class="layui-form" lay-filter="test">
  动态插入的表单域
</form>
<!-- import layui -->
<script>
layui.use(function(){
  var form = layui.form;
  // 当表单元素被动态插入时，需主动进行组件渲染才能显示
  form.render(); // 渲染全部表单
  form.render('select'); // 仅渲染 select 元素
  form.render(null, 'test'); // 仅渲染 lay-filter="test" 的容器内的全部表单
  form.render('checkbox', 'test'); // 仅渲染  lay-filter="test" 的容器内的 checkbox 元素
})
</script>
```

### **定向渲染**

该方法还允许指定表单元素的 jQuery 对象，从而完成定向渲染。且支持两种方式的指向：

- 若 jQuery 对象指向表单域容器（`class="layui-form"`），则渲染该表单域中的所有表单项；2.8+
- 若 jQuery 对象指向的不是表单域容器，则只对该对象进行渲染

定向渲染在页面出现大量表单时，可以极大地减少表单组件渲染时的性能开销，建议灵活运用。

```html
<div class="layui-form" id="form-id">
  <select id="select-id">
    <option value="a">A</option>
  </select>
  <!-- 其他表单元素 -->
</div>
<!-- import layui -->
<script>
layui.use('form', function(){
  var $ = layui.$;
  var form = layui.form;
  // 定向渲染（一般当表单存在动态生成时，进行渲染）
  // 传入需要渲染的相应表单元素的 jQuery 对象
  form.render($('#form-id')); // 渲染 id="form-id" 的表单域中的所有表单项
  form.render($('#select-id')); // 仅渲染 id="select-id" 的表单项
});
</script>
```

### 验证

Layui 对表单验证做了巧妙的支持，只需在表单元素上设置 `lay-verify=""` 属性值即可指定验证规则，如：

```html
<div class="layui-form">
  <input type="text" lay-verify="required" placeholder="必填项">
  <input type="text" lay-verify="email" placeholder="非必填项，但若有值则验证邮箱格式">
  <input type="text" lay-verify="required|number" placeholder="必填项，并验证数字格式">
  <button class="layui-btn" lay-submit>提交</button>
</div>
```

注：上述代码指定的均为内置的验证规则，具体可参考：[#属性介绍](https://layui.dev/docs/2/form/#attr)

### 自定义验证规则

```
form.verify(obj);
```

- 参数 `obj` 是一个对象，用于定义验证规则的集合。

除了内置的验证规则外，form 还允许自定义验证规则，规则以函数命名，返回的参数如下：

```html
// 自定义验证规则
form.verify({
  rule: function(value, elem) {
    console.log(value); // 当前进入验证的表单项的值
    console.log(elem); // 当前进入验证的表单项的 DOM 元素
  }
});
```

在自定义规则中，可根据规则函数返回的 value 自行判断是否必填，如：

```javascript
form.verify({
  // 必填项
  rule1: function(value, elem) {
    // 自定义规则
    if (value.length < 6) {
      return '不能小于 6 个字符';
    }
  },
  // 非必填项，只有当值填写时才验证自定义规则
  rule2: function(value, elem) {
    if (!value) return; // 若值未填写，不进行后续规则验证
    // 自定义规则
    if (/^[A-Z]/.test(value)) {
      return '必须用大写字符开头';
    }
  },
  // 自定义提示方式
  rule3: function(value, elem) {
    // 自定义规则和自定义提示方式
    if(value === 'xxx'){
      alert('用户名不能为敏感词'); // 此处以系统自带的 alert 提示方式为例
      return true; // 返回 true 即可阻止 form 默认的提示风格
    }
  }
});
```

####  自定义校验案例

lay-verify="password"     属性指定  = password 。

 校验方法中：又返回，就是不通过；没返回就是通过。

```html
<form class="layui-form">
  <input type="text" name="username" lay-verify="required|username" placeholder="用户名" class="layui-input">
  <hr>
  <input type="password" name="password" lay-verify="password" placeholder="密码" class="layui-input">
  <hr>
  <input type="text" name="motto" lay-verify="motto" placeholder="座右铭" class="layui-input">
  <hr>
  <button class="layui-btn" lay-submit lay-filter="demo-verify">提交</button>
</form>


<script>
layui.use(function(){
  var form = layui.form;
  // 自定义验证规则
  form.verify({
    // 验证用户名，且为必填项
    username: function(value, elem){
      if (!new RegExp("^[a-zA-Z0-9_\u4e00-\u9fa5\\s·]+$").test(value)) {
        return '用户名不能有特殊字符';
      }
      if (/(^_)|(__)|(_+$)/.test(value)) {
        return '用户名首尾不能出现下划线';
      }
      if (/^\d+$/.test(value)) {
        return '用户名不能全为数字';
      }
    },
    // 验证密码，且为必填项
    password: function(value, elem) {
      if (!/^[\S]{6,16}$/.test(value)) {
        return '密码必须为 6 到 16 位的非空字符';
      }
    },
    // 验证座右铭，且为非必填项
    motto: function(value, elem) {
      if (!value) return; // 非必填
      // 自定义规则
      if (!new RegExp("^[a-zA-Z0-9_\u4e00-\u9fa5\\s·]+$").test(value)) {
        return '座右铭不能有特殊字符';
      }
    }
  });
  // 提交事件
  form.on('submit(demo-verify)', function(data){
    var field = data.field; // 获取表单字段值
    // 显示填写结果，仅作演示用
    layer.alert(JSON.stringify(field), {
      title: '当前填写的字段值'
    });
    // 此处可执行 Ajax 等操作
    // …
    return false; // 阻止默认 form 跳转
  });
}) 
</script>

```

### 主动触发验证 2.7+

```
form.validate(elem);
```

- 参数 `elem` 为元素选择器或 jQuery 对象； 若验证通过，该方法将返回 true，否则返回 false

```
  <div class="layui-form-item">
    <label class="layui-form-label">手机</label>
    <div class="layui-input-block">
      <input type="tel" name="phone" lay-verify="required|phone" class="layui-input" id="validate-phone">
    </div>
  </div>
 <div class="layui-form-item">
    <label class="layui-form-label">验证码</label>
    <div class="layui-input-inline">
      <input type="text" name="vercode" lay-verify="required" class="layui-input">
    </div>
    <div class="layui-inline"> 
      <button type="button" class="layui-btn layui-btn-primary" id="validate-get-vercode">获取验证码</button>
    </div>
  </div>
  
  // 点击获取验证码
  $('#validate-get-vercode').on('click', function(){
    var isValid = form.validate('#validate-phone');  // 主动触发验证，v2.7.0 新增 
    // 验证通过
    if(isValid){
      layer.msg('手机号规则验证通过');
      // 此处可继续书写「发送验证码」等后续逻辑
      // …
    }
  });
```

## 赋值/取值

```
form.val(filter, obj);
```

- 参数 `filter` 为表单域容器（`class="layui-form"`）的 `lay-filter` 属性值
- 参数 `obj` 可选。若参数存在，则对表单域进行赋值；若参数不存在，则为对表单域进行取值。