# html标签

## 第一类  head等头部标签类

### 1 style 标签 

引用外部css ； 包裹css代码

```
<html>
<head>
<style type="text/css">
h1 {color:red}
p {color:blue}
</style>
</head>

<body>
<h1>Header 1</h1>
<p>A paragraph.</p>
</body>
</html>
```

### 2 title 标签

title 中的内容，显示在网页标签页上。

```
<html>
 
  <head>
    <title>XHTML Tag Reference</title>
  </head>

  <body>
    The content of the document......
  </body>

</html>
```



###  3  meta 标签

<meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。

```
<meta name="keywords" content="HTML,ASP,PHP,SQL">
```



### 4   <!--...--> 标签

  代码注释，浏览器不会执行。

```
<!--这是一段注释。注释不会在浏览器中显示。-->
```

### 5   <!DOCTYPE> 声明

DOCTYPE html 告诉浏览器文档类型 。<!DOCTYPE> 声明必须是 HTML 文档的第一行，位于 <html> 标签之前。

```
<!DOCTYPE html>
<html>
<head>
<title>文档的标题</title>
</head>

<body>
文档的内容......
</body>

</html>
```



### 6  a 标签 超链接

点击跳转到href的地址上。

```
<a href="http://www.w3school.com.cn">W3School</a>
```

### 7  html 标签

一个简单的 HTML 文档，带有最基本的必需的元素：

## 第二类 HTML 5 中的新标签。

### 1 main 标签

<main> 标签规定文档的主要内容。

<main> 元素中的内容对于文档来说应当是唯一的。它不应包含在文档中重复出现的内容，比如侧栏、导航栏、版权信息、站点标志或搜索表单。

**注释：**在一个文档中，不能出现一个以上的 <main> 元素。<main> 元素不能是以下元素的后代：<article>、<aside>、<footer>、<header> 或 <nav>。

### 2 nav 标签

<nav> 标签定义导航链接的部分。

```
<nav>
<a href="index.asp">Home</a>
<a href="html5_meter.asp">Previous</a>
<a href="html5_noscript.asp">Next</a>
</nav>
```

### 5   article  语义化标签  

<article> 标签规定独立的自包含内容。 
论坛帖子
报纸文章
博客条目
用户评论

```
<article>
  <h1>Internet Explorer 9</h1>
  <p>Windows Internet Explorer 9（简称 IE9）于 2011 年 3 月 14 日发布.....</p>
</article>
```

### 6 aside>语义化标签  

<aside> 标签定义其所处内容之外的内容。

aside 的内容应该与附近的内容相关。

```
<p>Me and my family visited The Epcot center this summer.</p>
<aside>
<h4>Epcot Center</h4>
The Epcot Center is a theme park in Disney World, Florida.
</aside>
```

### 7 head 标签

一个简单的 HTML 文档，带有最基本的必需的元素：

### 8  header  语义化标签

  ** <header> 标签定义文档的页眉（介绍信息）。

```
<header>
<h1>Welcome to my homepage</h1>
<p>My name is Donald Duck</p>
</header>

<p>The rest of my home page...</p>
```

### 

### link  标签

<link> 标签定义文档与外部资源的关系。

<link> 标签最常见的用途是链接样式表。

```
<head>
<link rel="stylesheet" type="text/css" href="theme.css" />
</head>
```

## 

##  第三类： 其他类标签

### 1  abbr标签

<abbr> 标签指示简称或缩写，比如 "WWW" 或 "NATO"。 主要用于注重浏览器搜索优化的项目。

```
The <abbr title="People's Republic of China">PRC</abbr> was founded in 1949.
```

### 2  audio 音频 

一段简单的 HTML 5 音频：

```
<audio src="someaudio.wav">
您的浏览器不支持 audio 标签。
</audio>
```

### 3 video 视频

```
<video src="movie.ogg" controls="controls">
您的浏览器不支持 video 标签。
</video>
```



### 4  b标签规定粗体文本。

```
<p>这是普通文本 - <b>这是粗体文本</b>。</p>
```

​       注释：根据 HTML5 规范，在没有其他合适标签更合适时，才应该把 <b> 标签作为最后的选项。HTML5 规范声明：应该使用 <h1> - <h6> 来表示标题，使用 <em> 标签来表示强调的文本，应该使用 <strong> 标签来表示重要文本，应该使用 <mark> 标签来表示标注的/突出显示的文本。

### 5 base 标签

head 头部内使用的标签。

<base> 标签为页面上的所有链接规定默认地址或默认目标。 <a>、<img>、<link>、<form> 标签中的 URL  

```
<head>
<base href="http://www.w3school.com.cn/i/" />
<base target="_blank" />
</head>

<body>
<img src="eg_smile.gif" />
<a href="http://www.w3school.com.cn">W3School</a>
</body>
```

### 6 button 标签

原生 按钮标签

```
<button type="button">Click Me!</button>
```

###  7 canvas 标签

<canvas> 标签只是图形容器，您必须使用脚本来绘制图形。

```
<canvas id="myCanvas"></canvas>

<script type="text/javascript">

var canvas=document.getElementById('myCanvas');
var ctx=canvas.getContext('2d');
ctx.fillStyle='#FF0000';
ctx.fillRect(0,0,80,100);

</script>
```



### 8  dl  dd列表

```
<h2>一个定义列表：</h2>

<dl>
   <dt>计算机</dt>
   <dd>用来计算的仪器 ... ...</dd>
   <dt>显示器</dt>
   <dd>以视觉方式显示信息的装置 ... ...</dd>
</dl>
```

### 8  ol li  有序列表

ul li 无序列表

```
<p>有序列表：</p>
<ol>
  <li>打开冰箱门</li>
  <li>把大象放进去</li>
  <li>关上冰箱门</li>
</ol>

<p>无序列表：</p>
<ul>
  <li>雪碧</li>
  <li>可乐</li>
  <li>凉茶</li>
</ul>
```



### 9   del 标签

定义文档中已被删除的文本。 **注释：**请与 <ins> 标签配合使用，来描述文档中的更新和修正。

```
<p>一打有 <del>80</del> <ins>90</ins> 件。</p>
```

### 10 details  标签

关于文档的细节：

与 [ 标签](https://www.w3school.com.cn/tags/tag_summary.asp) 配合使用可以为 details 定义标题。标题是可见的，用户点击标题时，会显示出 details。

```
<details>
<summary>Copyright 2011.</summary>
<p>All pages and graphics on this web site are the property of W3School.</p>
</details>
```

### 11  embed 标签

<embed> 标签定义嵌入的内容，比如插件。

```
<embed src="/i/helloworld.swf" />
```

### 12 fieldset> 标签

```

<form>
  <fieldset>
    <legend>健康信息</legend>
    身高：<input type="text" />
    体重：<input type="text" />
  </fieldset>
</form>

<p>如果表单周围没有边框，说明您的浏览器太老了。</p>
```

### 13  font 标签

<font> 规定文本的字体、字体尺寸、字体颜色。

```
<p><font color="red">A paragraph.</font></p>
```

### 14  footer  语义化 标签

<footer> 标签定义文档或节的页脚。

<footer> 元素应当含有其包含元素的信息。

页脚通常包含文档的作者、版权信息、使用条款链接、联系信息等等。

 您可以在一个文档中使用多个 <footer> 元素。



## form类

### 1 form  标签

<form> 标签用于为用户输入创建 HTML 表单。

表单能够包含 [input 元素](https://www.w3school.com.cn/tags/tag_input.asp)，比如文本字段、复选框、单选框、提交按钮等等。

表单还可以包含 [menus](https://www.w3school.com.cn/tags/tag_menu.asp)、[textarea](https://www.w3school.com.cn/tags/tag_textarea.asp)、[fieldset](https://www.w3school.com.cn/tags/tag_fieldset.asp)、[legend](https://www.w3school.com.cn/tags/tag_legend.asp) 和 [label 元素](https://www.w3school.com.cn/tags/tag_label.asp)。

表单用于向服务器传输数据。

### 2  input 标签

<input> 标签用于搜集用户信息。根据不同的 type 属性值，输入字段拥有很多种形式。输入字段可以是文本字段、复选框、掩码后的文本控件、单选按钮、按钮等等。

## table类

### 1  textarea  标签

<textarea> 标签定义多行的文本输入控件。

### 2 table 标签

table tr th td组合使用

```
<table border="1">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>
```

更加语义化 head body foot

```
<table border="1">
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>

  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>

  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
</table>
```

## 其他

### 1  frame  标签

frameset 元素可定义一个框架集 。 组合使用

三列分

```
<frameset cols="25%,50%,25%">

  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">

</frameset>
```

###  2  iframe 标签

iframe 元素会创建包含另外一个文档的内联框架（即行内框架）。

### 3  h1 - h6

标签可定义标题。<h1> 定义最大的标题。<h6> 定义最小的标题。

由于 h 元素拥有确切的语义，不要仅仅为了产生粗体文本而使用它们。请使用其它标签或 CSS 代替。

### 4  hr  标签  分割线

```
<h1>This is header 1</h1>
<hr />
<p>This is some text</p>
```



### 5  i 标签

<i> 标签显示斜体文本效果。



### 6  img 标签

```
<img src="/i/eg_tulip.jpg"  alt="上海鲜花港 - 郁金香" />
```



### 7  label 标签

<label> 标签为 input 元素定义标注（标记）。label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。 

效果就是：点击label, label for对应的input会被选中。

```
<form>
  <label for="male">Male</label>
  <input type="radio" name="sex" id="male" />
  <br />
  <label for="female">Female</label>
  <input type="radio" name="sex" id="female" />
</form>
```

### 8 mark 标签

<mark> 标签定义带有记号的文本。请在需要突出显示文本时使用 <m> 标签。

### 9  meter 标签 进度条



```
<p>显示度量值：</p>
<meter value="3" min="0" max="10">3/10</meter><br>
<meter value="0.6">60%</meter>

<p><b>注释：</b>Internet Explorer 不支持 meter 标签。</p>
```

### progress 进度条

```
<progress value="22" max="100"></progress> 

下载进度：
<progress value="22" max="100">
</progress>

<p><b>注释：</b>Internet Explorer 9 以及更早的版本不支持 <progress> 标签。</p>
```



### 11   分组下拉

optgroup 元素用于组合选项。当您使用一个长的选项列表时，对相关的选项进行组合会使处理更加容易。

```
<select>
  <optgroup label="Swedish Cars">
    <option value ="volvo">Volvo</option>
    <option value ="saab">Saab</option>
  </optgroup>

  <optgroup label="German Cars">
    <option value ="mercedes">Mercedes</option>
    <option value ="audi">Audi</option>
  </optgroup>
</select>
```

### 12 一般下拉

```
<select>
  <option value ="volvo">Volvo</option>
  <option value ="saab">Saab</option>
  <option value="opel">Opel</option>
  <option value="audi">Audi</option>
</select>
```

### 13 img图片的自适应标签

 有媒体查询的作用

```
<h1>picture 元素</h1>

<p>请调整浏览器窗口的大小以加载不同的图像。</p>

<picture>
  <source media="(min-width:650px)" srcset="/i/photo/flower-4.jpg">
  <source media="(min-width:465px)" srcset="/i/photo/tulip.jpg">
  <img src="/i/photo/flower.gif" alt="Flowers" style="width:auto;">
</picture>
```

### 14

pre 元素可定义预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。

### 15 q  标签  引用符号

标记短的引用：

```
<q>Here is a short quotation here is a short quotation</q>
```

### 16  sub  标签 下标

```
这段文本包含 <sub>下标</sub>
```

### 17  sup标签 上标

### 18 svg  标签

SVG 有几种绘制路径、框、圆、文本和图形图像的方法。

```
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>
```

### 19  template  标签

使用 <template> 保留页面加载时隐藏的内容。使用 JavaScript 来显示：

```
<!DOCTYPE html>
<html>
<body>

<h1>template 元素</h1>

<p>单击下面的按钮，显示 template 元素中的隐藏内容。</p>

<button onclick="showContent()">显示隐藏的内容</button>

<template>
  <h2>Flower</h2>
  <img src="/i/photo/flower.gif" width="180" height="180">
</template>

<script>
function showContent() {
  var temp = document.getElementsByTagName("template")[0];
  var clon = temp.content.cloneNode(true);
  document.body.appendChild(clon);
}
</script>

</body>
</html>
```





## HTML5  原来有的

- button
- checkbox
- date
- datetime
- datetime-local
- email
- file
- hidden
- image
- month
- number
- password
- radio
- range
- reset
- submit
- text
- time
- url
- week

## 新的 Input 类型

- color
- date
- datetime
- datetime-local
- email
- month
- number
- range
- search
- tel
- time
- url
- week



