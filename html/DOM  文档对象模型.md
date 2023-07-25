# DOM  文档对象模型

### 1  Attr 对象

在 HTML DOM （文档对象模型）中，每个部分都是节点：

- 文档本身是文档节点
- 所有 HTML 元素是元素节点
- 所有 HTML 属性是属性节点
- HTML 元素内的文本是文本节点
- 注释是注释节点

### 2 Document  对象

每个载入浏览器的 HTML 文档都会成为 Document 对象。

Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

#####  对象集合:

```
all[]	提供对文档中所有 HTML 元素的访问。
anchors[]	返回对文档中所有 Anchor 对象的引用。
applets	返回对文档中所有 Applet 对象的引用。
forms[]	返回对文档中所有 Form 对象引用。
images[]	返回对文档中所有 Image 对象引用。
links[]	返回对文档中所有 Area 和 Link 对象引用。
```

##### 对象属性:

```
body 提供对 <body> 元素的直接访问。

对于定义了框架集的文档，该属性引用最外层的 <frameset>。

cookie	设置或返回与当前文档有关的所有 cookie。
domain	返回当前文档的域名。
lastModified	返回文档被最后修改的日期和时间。
referrer	返回载入当前文档的文档的 URL。
title	返回当前文档的标题。
URL	返回当前文档的 URL。
```



#####  对象方法:

```
close()	关闭用 document.open() 方法打开的输出流，并显示选定的数据。
getElementById()	返回对拥有指定 id 的第一个对象的引用。
getElementsByName()	返回带有指定名称的对象集合。
getElementsByTagName()	返回带有指定标签名的对象集合。
open()	打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出。
write()	向文档写 HTML 表达式 或 JavaScript 代码。
writeln()	等同于 write() 方法，不同的是在每个表达式之后写一个换行符。
```

### 3 Element 对象

在 HTML DOM 中，Element 对象表示 HTML 元素。

Element 对象可以拥有类型为元素节点、文本节点、注释节点的子节点。

NodeList 对象表示节点列表，比如 HTML 元素的子节点集合。

元素也可以拥有属性。属性是属性节点（参见下一节）。

#### 属性和方法

下面的属性和方法可用于所有 HTML 元素上：

```
方法和属性的功能包含： 
 获取dom的子节点，父节点，高度，宽度，是否包含指定节点，是否包含或添加指定属性（class id data-v )
 方法包含: 删除节点，修改节点，添加节点，
```

### 4 DOM 事件

HTML DOM 事件允许 JavaScript 在 HTML 文档中的元素上注册不同的事件处理程序。

事件通常与函数结合使用，在事件发生之前函数不会被执行（例如当用户单击按钮时）。

事件分类： 

#### [Event](https://www.w3school.com.cn/jsref/obj_event.asp)  对象 :

DOM 中的所有事件对象都基于 Event 对象。

因此，所有其他事件对象（如 [MouseEvent](https://www.w3school.com.cn/jsref/obj_mouseevent.asp) 和 [KeyboardEvent](https://www.w3school.com.cn/jsref/obj_keyboardevent.asp)）都可以访问 Event 对象的属性和方法。

#### AnimationEvent 对象 ：

 CSS 动画运行时发生的事件属于 AnimationEvent 对象。

#### ClipboardEvent 对象

剪贴板被修改时发生的事件，属于 ClipboardEvent 对象。

#### FocusEvent 对象

当元素获得或失去焦点时发生的事件属于 FocusEvent 对象。

#### KeyboardEvent 对象	

当用户按下键盘上的某个键时发生的事件属于 KeyboardEvent 对象。

#### MouseEvent 对象

鼠标与 HTML 文档交互时发生的事件属于 MouseEvent 对象。

#### PageTransitionEvent 对象

当用户导航到和离开网页时发生的事件。

#### UiEvent 对象

从用户界面触发的事件属于 UiEvent 对象。

#### TouchEvent 对象

当用户触摸基于触控的设备时发生的事件属于 TouchEvent 对象。

### 5 Location 对象

Location 对象包含有关当前 URL 的信息。

Location 对象是 Window 对象的一个部分，可通过 window.location 属性来访问。

#### 属性

| [hash](https://www.w3school.com.cn/jsref/prop_loc_hash.asp)  | 设置或返回从井号 (#) 开始的 URL（锚）。       |
| ------------------------------------------------------------ | --------------------------------------------- |
| [host](https://www.w3school.com.cn/jsref/prop_loc_host.asp)  | 设置或返回主机名和当前 URL 的端口号。         |
| [hostname](https://www.w3school.com.cn/jsref/prop_loc_hostname.asp) | 设置或返回当前 URL 的主机名。                 |
| [href](https://www.w3school.com.cn/jsref/prop_loc_href.asp)  | 设置或返回完整的 URL。                        |
| [pathname](https://www.w3school.com.cn/jsref/prop_loc_pathname.asp) | 设置或返回当前 URL 的路径部分。               |
| [port](https://www.w3school.com.cn/jsref/prop_loc_port.asp)  | 设置或返回当前 URL 的端口号。                 |
| [protocol](https://www.w3school.com.cn/jsref/prop_loc_protocol.asp) | 设置或返回当前 URL 的协议。                   |
| [search](https://www.w3school.com.cn/jsref/prop_loc_search.asp) | 设置或返回从问号 (?) 开始的 URL（查询部分）。 |

#### Location 对象方法

| [assign()](https://www.w3school.com.cn/jsref/met_loc_assign.asp) | 加载新的文档。           |
| ------------------------------------------------------------ | ------------------------ |
| [reload()](https://www.w3school.com.cn/jsref/met_loc_reload.asp) | 重新加载当前文档。       |
| [replace()](https://www.w3school.com.cn/jsref/met_loc_replace.asp) | 用新的文档替换当前文档。 |

### 5 Navigator 对象

获取浏览器的 名字 版本号 操作系统平台。 等信息

### 6 Screen 对象

Screen 对象包含有关客户端显示屏幕的信息

| [availHeight](https://www.w3school.com.cn/jsref/prop_screen_availheight.asp) | 返回显示屏幕的高度 (除 Windows 任务栏之外)。 |
| ------------------------------------------------------------ | -------------------------------------------- |
| [availWidth](https://www.w3school.com.cn/jsref/prop_screen_availwidth.asp) | 返回显示屏幕的宽度 (除 Windows 任务栏之外)。 |

获取高度 宽度，像素点等数据。

###  7 Style 对象

Style 对象代表一个单独的样式声明。可从应用样式的文档或元素访问 Style 对象。

使用 Style 对象属性的语法：

```
document.getElementById("id").style.property="值"
```

读取样式

```
  var box = document.getElementById("myList");
    var boxStyle = window.getComputedStyle(box,null);
    console.log(boxStyle.width);//100px
```

### 8 Window 对象

Window 对象表示浏览器中打开的窗口。

如果文档包含框架（frame 或 iframe 标签），浏览器会为 HTML 文档创建一个 window 对象，并为每个框架创建一个额外的 window 对象。

属性有：

parent  返回父窗口。

innerheight  返回窗口的文档显示区的高度。

history  对 History 对象的只读引用。请参数 [History 对象](https://www.w3school.com.cn/jsref/dom_obj_history.asp)。

 返回窗口的文档显示区的高度 [innerheight](https://www.w3school.com.cn/jsref/prop_win_innerheight_innerwidth.asp)

返回窗口的文档显示区的宽度。 [innerwidth](https://www.w3school.com.cn/jsref/prop_win_innerheight_innerwidth.asp)



# webAIP  BOM 浏览器对象

### 1 Console 

对象提供对浏览器调试控制台的访问。

常用的 log  info table 等等

### 2 History 对象

History 对象包含用户（在浏览器窗口中）访问过的 URL。

History 对象是 window 对象的一部分，可通过 window.history 属性对其进行访问。

属性

[length](https://www.w3school.com.cn/jsref/prop_his_length.asp)  返回浏览器历史列表中的 URL 数量。

对象方法

| [back()](https://www.w3school.com.cn/jsref/met_his_back.asp) | 加载 history 列表中的前一个 URL。   |
| ------------------------------------------------------------ | ----------------------------------- |
| [forward()](https://www.w3school.com.cn/jsref/met_his_forward.asp) | 加载 history 列表中的下一个 URL。   |
| [go()](https://www.w3school.com.cn/jsref/met_his_go.asp)     | 加载 history 列表中的某个具体页面。 |

### 3 Storage 对象

Web Storage API 的 Storage 对象提供对特定域的会话存储或本地存储的访问。这使您可以读取、添加、修改和删除存储的数据项。

| [key(*n*)](https://www.w3school.com.cn/jsref/met_storage_key.asp) | 返回存储中第 n 个键的名称。                  |
| ------------------------------------------------------------ | -------------------------------------------- |
| [length](https://www.w3school.com.cn/jsref/prop_storage_length.asp) | 返回存储在 Storage 对象中的数据项的数量。    |
| [getItem(*keyname*)](https://www.w3school.com.cn/jsref/met_storage_getitem.asp) | 返回指定键名的值。                           |
| [setItem(*keyname*, *value*)](https://www.w3school.com.cn/jsref/met_storage_setitem.asp) | 将键添加到存储中，或更新键的值（若已存在）。 |
| [removeItem(*keyname*)](https://www.w3school.com.cn/jsref/met_storage_removeitem.asp) | 从存储中删除键。                             |
| [clear()](https://www.w3school.com.cn/jsref/met_storage_clear.asp) | 清空存储中的所有键。                         |

## 4 Geolocation 对象

Geolocation 对象允许用户向 Web 应用程序提供其位置。出于隐私原因，会要求用户允许报告位置信息。