# scss的基本用法

功能： css代码，js化。提供复用。

## **一、使用变量**

### **1. 变量声明**

```
$ + 字母 ：加颜色值或其他css的值
$color-base:#00c16f 
$border-base:1px solid black;
```

### **2.变量引用**

　凡是 CSS 属性的标准值（比如说1px或者bold）可存在的地方，变量就可以使用。CSS 生成时，变量会被它们的值所替代。如果你需要一个不同的值，只需要改变这个变量的值，则所有引用此变量的地方生成的值都会随之改变。

```css
<style lang='scss'>
  $color-base : #00c16f 
 .aaa{
    color:$color-base
 }


```

### **3.变量的作用域**

1.顶级的变量，后面都可以使用。

2.像 .bbb种定义的为局部，自己和其后代可以使用。同级不能使用。

```css
<style lang='scss'>
  $color-base : #00c16f 
 .aaa{
    color:$color-base;
     
 }
  .bbb{
        $base-border:1px solid red;
        
        .b1{
            border:$base-border
        }
    }
```

### **4.变量名用中划线还是下划线分隔**

$color_base和$color-base其实指向的是同一个变量。　　　　

其实在 **sass** 的大多数地方，中划线命名的内容和下划线命名的内容是互通的，除了变量，也包括对混合器和 Sass 函数的命名。但是在 **sass** 中纯 **css** 部分不互通，比如类名、ID或属性名。

## **二.嵌套CSS规则**

在Sass中，你可以像俄罗斯套娃那样在规则块中嵌套规则块。**sass** 在输出 **css** 时会帮你把这些嵌套规则处理好，避免你的重复书写

```
.aaa{
   div{
       xxxx
    }
}

```

## **1.父选择器的标识符&**

最常见的一种情况是当你为链接之类的元素写`：hover`这种伪类时，你并不希望以后代选择器的方式连接

```
     .aaa div{
　　　　　background:red;
　　　　　&:hover{ background:blue;}
　　}
```

   &指代夫选择器div.解析时，会替换掉。如下

```
　.aaa div{ background:red;}
  .aaa div:hover{ background:blue;}
```

## **2.群组选择器的嵌套**

```
.aaa{
 h1,h2,h3{  color:red }
}

.bbb, .ccc{
 font-size:30px
}
```

## **3.子组合选择器和同层组合选择器：>、+ 和 ~**

![](.\img\css1_20240429220053.png)

这些组合选择器可以毫不费力地应用到`sass`的规则嵌套中。可以把它们放在外层选择器后边，或里层选择器前边：

![](.\img\css2_20240429220230.png)

## 　**4.嵌套属性**

案例1

正常css

```
nav{
   border-style:solid;
   border-width:1px;
   border-color:#ccc
}
```

scss写法

```
nav{
   border:{
      style:solid;
      width:1px;
      color:#ccc
   }
}
```

案例2

正常css

```
nav{
border:1px solid red;
border-left: 0px;
border-right:0px
}
```

scss写法

```
border:1px  solid red{
    left:0px;
    right:0px
}
```

这里有个小坑，border冒号后面要加空格，不然会报错，说border:后的css无效这比下边这种同等样式的写法要好.

## **三. 导入SASS文件**

### **1.使用SASS部分文件**

```

<style lang"scss">
@import'../../static/css/hello world.scss';  //这个样式文件成为局部样式
组件中可以引入样式文件，该样式会打包进这个组件样式中。   
```

### **2. 默认变量值**

 1.变量覆盖：

```
$link-color:blue;
$link-color:red;
a{
  color:$link-color
}
和js变量覆盖效果一样，这个最后是red;
```

2.关键字

```
<style lang"scss">
  @import'../../static/css/hello world.scss';  
  假如：局部文件中，包含一个 $font-size-base:20px!default;
 
 $font-size-base:30px;     组件中写了同样变量的样式，则使用自己的，没有就使用引入的默认值。
```

### **3.嵌套导入**

```
<template>
<template>
<style lang"scss">



aside{
   @import'../../static/css/hello world.scss';  
}
 此时，局部样式表，只在aside中起作用。
<style>
```

**4.原生的CSS导入**

## **四.静默注释**

```
body{
  color:red;   //这种注释内容不会出现在生成的css文件中
  padding:0;  /*这种注释内容会出现在生成的css文件中*/
}

```

## **五.混合器**

### 1.实现大段样式的重用

定义重复样式块

```css
@mixin blend-button{
  width:100px;
  height:50px;
}
```

使用样式块

```css
button{
  @include blend-button;
  background:yellow;
}
```

最后解析成：

```css
button{
  width:100px;
  height:50px;
  background:yellow;
}
```

### **2.混合器中的CSS规则**

混合器中不仅可以包含属性，也可以包含`css`规则，包含选择器和选择器中的属性。当一个包含`css`规则的混合器通过`@include`包含在一个父规则中时，在混合器中的规则最终会生成父规则中的嵌套规则。混合器中的规则甚至可以使用`sass`的父选择器标识符`&`。使用起来跟不用混合器时一样，`sass`解开嵌套规则时，用父规则中的选择器替代`&`。

![](.\img\css3.png)



### 　**3.给混合器传参**

```css
@mixin blend-button( $width ){
  width:$width/2 ;     <---- 传入的参数，也能简单计算
  height:50px;
}



button{
  @include blend-button( 200px );
  background:yellow;
}

也可以传入多个值 ， 号隔开。
```

### **4.默认参数值**





### 5.条件混合器

```html
<div class="mixin3">mixin3</div>
```



```css
@mixin option($option) {
  @if $option==1 {
    color: yellow;
  }
  @else if $option==2 {
    color: green;
  }
  @else {
    color: black;
  }
}
.mixin3 {
  @include option(2);
}
```



# SCSS嵌套语法规则 （待总结）

https://blog.csdn.net/qq_18149105/article/details/136654988
