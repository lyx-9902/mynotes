# Web Components 

摘抄  https://zhuanlan.zhihu.com/p/580540604

## **1. Web Components 是什么？**

Web Components 是一套不同的技术，允许您创建可重用的定制元素（它们的功能封装在您的代码之外）并且在您的 web 应用中使用它们。Web Components 也是一个浏览器原生支持的组件化方案，允许你创建新的自定义、可封装的HTML 标记，使用时不用加载任何额外的模块。自定义组件和小部件基于 Web Components 标准构建，可跨现代浏览器工作，并可与任何支持 HTML 的 JavaScript 库或框架一起使用。

其实简单理解 Web Components 就是：**Web Components 是一套技术，允许创建可重用的自定义元素**

而 Web Component 的目的也很明确，从`原生层面实现组件化，使开发者开发、复用、扩展自定义组，实现自定义标签`。意味着前端开发人员开发组件时可以实现 `Write once, run anywhere`。

### **Web Components 的组成**

Web Components 本身不是一个单独的规范，也不是一门单一的技术，而是由一组 DOM API 和 HTML 规范所组成。它其中就包含了：

- ES Modules
- HTML templates
- Custom Elements
- Shadow DOM

### **ES Modules**

ES Modules（ESM）相信大家非常熟悉了，作为组件的引入方式成为 Web Components 的规范之一。其实早期并不是使用的 ES Modules 作为 Web Components 的导入方式，而是 HTML Imports，可惜 HTML Imports 已经被废弃，如果想正常使用 HTML Imports 代码查看效果，可以安装低版本浏览器。

ES Modules（ESM）使 Web Components 能够以模块化方式开发，这与其他接受的 JavaScript 应用程序开发实现保持一致。您可以在 JS 文件中定义自定义元素的接口，然后将其包含在 type="module" 属性中。

### **HTML templates**

HTML templates 利用 template 进行元素包裹，包裹的元素不会立即渲染，只有在内容有效的时候，才会解析渲染，具有这个属性后，我们可以在自定义标签中按需添加我们需要的模板，并在自定义标签渲染的时候再去解析我们的模板，这样做可以在 HTML 有频繁更改更新任务，或者重写标记的时候非常有用。

### **Custom elements**

Custom elements 通过 CustomElementRegistry 来自定义可以直接渲染的 html 元素，并提供了组件的生命周期 `connectedCallback`、`disconnectCallback`、`attributeChangedCallback` 等提供给开发者聚合逻辑时使用。

### **Shadow DOM**

Shadow Dom 被称为 影子DOM」 或 「隐式 DOM」，顾名思义，具有隐藏属性，具体的意思就是说，在使用 Shadow DOM 的时候，组件标签内的 CSS 和 HTML 会完全的隐式存在于元素内部，在具体页面中，标签内部的HTML 结构会存在于 `#shdaow-root`，而不会在真实的 dom 树中出现。其实这个 Shadow Dom并不陌生，在前端开发时使用的很多 HTML 标签中已经将它运用起来。例如常见的 `video`标签。

## **2. Web Components 的历史**

其实 Web Components 并不是近几年才出现的规范。

最早在 2011 年的时候 Google 就推出了 Web Components 的概念，也算是前端发展的早期了。那时候前端还处于百废待兴的一个状态，前端甚至都没有「组件化」的概念，但是就是这个时候 Google 就已经凭明锐的嗅觉察觉到「组件化」是未来发展的趋势，所以提出了 Web Components 。不过在最开始时 Google 也只是提出了这样一个概念，并没有去实现它，所以并没有出现太大的浪花。

> 2011 年 React 框架也诞生了。

到了 2013 年，Google 浏览器和 Opera 浏览器联合推出 Web Components 规范的 v0 版本。这也算是 Web Components 最早的版本了。

> 2013 年 React 框架开源。
> 2014 年 Vue 框架诞生，这里为什么要提到 Vue 框架了？因为 Vue 作者在创建 Vue 的时候大量参考了 Web Components 的语法。

在 2016 年 2 月， Shadow DOM 和 Custom Element 被并入 DOM 标准规范里面，而不再作为独立的规范存在。

在 2017 年 Google I/O 上，Polymer 框架发布2.0 版本，而这次升级的最主要意义就是将 Shadow Dom 和 Custom Elements 升级到 v1 版本，从而获得更多浏览器支持下一 代 Web Components 规范。

然后在 2018 年，Shadow DOM 和 Custom Element v2 在 Chrome、Safari、三星浏览器上已经支持，还被 Firefox 列为要支持的特性。

所以 Web Components 并不是一个新的概念，它已经存在很长时间了，只是可能还没有全面的进入研发者的视野。

## **3.Web Components 发展趋势**

尽管 Web Components 可能还没有全面的进入研发者的视野，现在还备受争议，但是它已经被很多大厂已经直接或者间接将它用于实践，比如：Twitter、YouTube、Electronic Arts、Adobe Spectrum、IBM 等等大厂（当然不止于此）。

在 Chrome 浏览器中对 customElements.define 至少调用一次的页面加载百分比统计也可看出 Web Components 已经相当流行。

并且在市场上也出现了很多 Web Components 库，可以轻松的使用和构建 Web Components，例如：

- **hybrids**： 是一个 JavaScript UI 框架，用于创建功能齐全的 Web 应用程序、组件库或具有独特的混合声明性和功能性架构的单个 Web Components。
- **LitElement**： 是一个简单的基类，用于使用 lit-html 创建快速、轻量级的 Web Components。
- **Polymer** ：是 Google 推出的 Web Components 库，支持数据的单向和双向绑定，兼容性较好，跨浏览器性能也较好；提供了一组用于创建 custom elements 的功能。这些功能旨在使 custom elements 像标准 DOM 元素一样工作更容易和更快。
- **X-Tag**： 是微软推出的开源库，支持 Web Components 规范，兼容Web Components API。
- **Slim.js**： 是一个开源的轻量级 Web Components 库，它为组件提供数据绑定和扩展能力，使用 es6 原生类继承。专注于帮助开发者更好的编写原生web组件，而不依赖于其他框架，但是也提供了良好的拓展性，开发者可以自由拓展。
- **Stencil**： 是一个用于构建可重用、可扩展的设计系统的工具链。生成可在每个浏览器中运行的小型、极快且 100% 基于标准的 Web Components。
- **Omi**： 是 Web Components + JSX/TSX 融合为一个框架，小巧的尺寸和高性能，融合和 React 和 Web Components 各自的优势

## **4. Web Components 的优势**



随着前端的发展，前端以 React、Vue、Angular 为主的框架也日益完善，大家肯定很奇怪，现在的前端框架不是挺好的吗？为什么我们还需要 Web Components 了? 最大的原因在于 Web Components 建立在 Web 标准之上。

虽然框架组件很棒，但它们只在自己的生态系统中很棒。您不能（轻松）在 React 中使用 Angular 组件，也不能（轻松）在 React 中使用 Vue 组件，反之亦然。而 Web Components 建立在 Web 标准之上，它们将可以在所有生态系统中工作，这也决定了它有巨大的优势：

- 互操作性：组件可以超越框架并用于不同技术栈的多个项目中。
- 组件寿命：组件是可互操作的，这也决定了 Web Components 的组件寿命会更长，并不需要考虑技术栈版本升级到来的不兼容问题。
- 可移植性：组件可以在几乎没有依赖关系的任何地方工作。由于它是原生，使用障碍明显低于组件依赖库或框架



![土拍你](https://pic4.zhimg.com/80/v2-51764f511fc94d944ec7c6f83a82330b_720w.webp)

**除此之外，Web 组件还具有向下的交叉兼容性，这对于随着不断变化的 Web 环境向前发展至关重要。**

## **5. Web Components 的限制**

虽然 Web Components 有着巨大的优势，但是也存在一些限制，如果你正在使用它，那请注意了。例如：

- Web Components 提供的 `CSS 封装是有限`。
- 虽然能实现 CSS 的隔离，但是隔离也会导致和`外部 CSS 交互比较难`。
- `Object.prototype.toString`不返回与原生对象相同的字符串。
- `document` 、 `window`、` document.body`、` document.head`是不可配置的，不能被覆盖。
- 未实现跨窗口/框架访问。
- CSS:host()规则在其参数选择器中只能（最多）有一层嵌套括号。例如，:host(.zot)两者:host(.zot:not(.bar))都有效，但:host(.zot:not(.bar:nth-child(2)))没有。

## **最后**

Web Components 优势明显，能彻底改变 Web 的开发，但是目前来说还需时日，需要做大量工作才能使 WebComponents 变得真正优秀，才能让大家享受到「组件化」 Web 开发的便利。但请大家不要混淆，Web Components 并不是为了取代任何现有框架而生，Web Component 的目的是为了从`原生层面实现组件化，可以使开发者开发、复用、扩展自定义组件，实现自定义标签`，解决 Web 组件的重用和共享问题，并使 Web 生态保持持续的开放和统一。





