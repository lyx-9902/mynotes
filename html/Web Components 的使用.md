## 如何使用Web Components

## 1.演示定义一个Hello World组件

这里演示定义一个Hello World组件，网页只要插入下面代码，就会在页面显示Hello World组件

```xml
<hello-world></hello-world>
```

完整代码，test-01.html

```javascript
<!DOCTYPE html>

<html>
    <head><title>test-01</title></head>
    <body>
        <h4>test-01</h4>

        <!-- 这里使用自定义的web components -->
        <hello-world url='我是组件传参'></hello-world>

        <!-- 自定义web components视图样式 -->
        <template id="testTemplate01">
            <style>
                #title {
                  color: red;
                }
            </style>
            <span id="title">Hello Web Components !</span>
        </template>

        <script>

            // web components定义 需要继承HTMLElement类
            class HelloWorld extends HTMLElement {
                constructor() {
                    super();
                    // 获取页面上的template
                    const template = document.querySelector('#testTemplate01');
                    // 克隆节点，防止该组件被多处使用时，修改了一处，其他地方也跟着变化
                    // 参数true表示递归克隆子元素
                    const content = template.content.cloneNode(true);
                    this.appendChild(content);
					console.log(this.getAttr('url'))//获取组件传参
                }
				getAttr(attr){//定义类方法
					return this.getAttribute(attr)
				}
            }

            window.onload = () => {
                // 注册web components
                window.customElements.define('hello-world', HelloWorld);
            };
        </script>
    </body>
</html>
```

使用浏览器打开test-01.html，页面展示如下

![图片](//upload-images.jianshu.io/upload_images/27234796-1702d30aacea394b.png)

上面示例定义了一个简单的Hello World组件，使用过Vue的同学会觉得上面的写法似曾相识，但它并没有使用第三方框架，完全使用浏览器原生API完成。

相较于Vue、React、Angular 等框架定义的组件，web components扩展性更好，不会因为Vue2.x变更到Vue3.x导致组件不能使用。

对上面的API做一些说明：

1. `<template>`标签

   `<template>`标签用于定义web components的内容和样式，`<template>`包裹的元素不会立即渲染，只有在内容有效的时候，才会解析渲染，具有这个属性后，我们可以在自定义标签中按需添加我们需要的模板，并在自定义标签渲染的时候再去解析我们的模板，这样做可以在 HTML 有频繁更改更新任务，或者重写标记的时候非常有用。

2. `customElements.define()`函数

   自定义元素需要使用 JavaScript 定义一个类，并且继承HTMLElement，这样一来，自定义元素便继承了HTML元素的特性，然后使用浏览器原生的`customElements.define()`函数，告诉浏览器`<hello-world>`标签与自定义类关联

   

   ```dart
   window.customElements.define('hello-world', HelloWorld);
   ```

更多API说明可以到官网查阅[Web Components API](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.webcomponents.org%2Fintroduction)

## 2.Web Components如何应用于生产？

上面的示例只是一个简单的演示，如果要应用于生产还有许多额外的知识需要进行学习，例如绑定事件，使用插槽，动态数据绑定等。

不过，大部分情况下我们并不需要使用原生API创建Web Components，因为代码量相对较大，市面上已经出现了很多库，可以更加轻松的使用和构建Web Components。

- [Polymer](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FPolymer%2Fpolymer) ：Google推出的Web Components库，支持数据的单向和双向绑定，兼容性较好，跨浏览器性能也较好；提供了一组用于创建 custom elements 的功能。这些功能旨在使custom elements 像标准 DOM 元素一样工作更容易和更快。
- [X-Tag](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fx-tag%2Fcore)： 是微软推出的开源库，支持Web Components规范，兼容Web Components API。
- [Stencil](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fionic-team%2Fstencil)： 是一个用于构建可重用、可扩展的设计系统的工具链。生成可在每个浏览器中运行的小型、极快且100%基于标准的Web Components。
- [hybrids](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fhybridsjs%2Fhybrids)： 是一个 JavaScript UI 框架，用于创建功能齐全的 Web 应用程序、组件库或具有独特的混合声明性和功能性架构的单个Web Components。
- [LitElement](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Flit%2Flit-element)： 是一个简单的基类，用于使用lit-html创建快速、轻量级的Web Components。

[Polymer] start最多(21.9k)，而且有大厂支持，是一个不错的选择。



## 3.前端发展方向

Web Components已经被很多大厂直接或者间接地用于实践，比如：Twitter、YouTube、Electronic Arts、Adobe Spectrum等。

有些同学可能会产生疑问，现在的前端框架不是挺好的吗？为什么还需要Web Components?

最大的原因在于Web Components是建立在Web标准之上。

虽然现在许多前端框架组件都很不错，用起来也很方便，但它们只在自己的生态系统中很不错。但你不能（轻松）在 React 中使用 Angular 组件，也不能（轻松）在 React 中使用 Vue 组件。而Web Components 建立在Web标准之上，它可以在所有生态系统中工作，这是第三方框架无法比拟的优势。