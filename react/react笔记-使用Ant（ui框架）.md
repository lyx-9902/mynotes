

## react使用 Ant ui框架

说明：Ant Design 是一个 ui框架，和 bootstrap 一样是ui框架。里面的组件很完善，开发中后台系统非常方便。分别基于react、vue、angular框架，各自开发了一套 Ant Design 的UI框架。（这里主要讲react框架的 Ant Design）

   系列          框架          系列官方命名

Ant:   |——  react        Ant Design    (n. (design) 设计；图案)

​          |——  vue          Ant Design Vue

​          |—— angular    ng-zorro



​          |——     移动端     Ant Design Mobile    一个基于 Preact / React / React Native 的 UI 组件库

1. Ant Design 是蚂蚁金服开发和正在使用的一套企业级的前端设计语言和基于 [React](http://www.oschina.net/p/facebook-react) 的前端框架实现。最早是在2015年发布的。
2. 对react 评价： React 本身的 API 并不多，是一个较为简单的框架。但是，要用好它，必须使用其他的配套工具，所以人们常说学习 React 并不是学习一个框架，而是学习一整套 React 技术栈。



扩展新闻：

1. React.js   是Facebook 开发所有。自2016 爆发React专利事件
   2. Twitter公司开源的Bootstrap
      3. Ant 目前还没有官方的  针对 vue移动端  版本 ui



注意： Ant 有针对react  vue  移动端，pc端 ，注意区分

### 按钮 案例演示

   **antd官网**    https://ant.design/docs/react/introduce-cn

#### 1. npm 下载

```javascript
npm install antd --save    /   yarn add antd     /  cnpm install antd --save
```

#### 2  在react项目的css文件中引入Antd的css

```javascript
@import '~antd/dist/antd.css';    //引入index.css
注意： index.js 中也要有引入   
import './index.css';
```

3)、 案例： 如何使用一个Button:



#### a在对应的组件中引入Antd

```javascript
import { Button } from 'antd';
```

#### 在html本分写

```javascript
<Button type="primary">Primary</Button>
  
```

#### 查看页面，已经显示了.

```javascript
import React from 'react';
import {Card,Button} from 'antd'


const App  = function(){

  function eventclick(e){
console.log(e);
  }
return(

        <div className="App">
        <div>
          <button>我是原生</button>
          <Card title="普通的按钮">
            <Button> 无样式按钮 </Button>
            <Button type="primary" onClick = { eventclick}> 普通按钮 </Button>
            <Button type="dashed"> 虚线按钮 </Button>
            <Button type="danger"> 危险按钮 </Button>
            <Button disabled> 被禁用的按钮 </Button>
          </Card>
        </div>
      </div>
      )

}




export default App;

```

**eact中使用Antd高级配置，按需引入css样式**
现在组件已经成功运行起来了，但是在实际开发过程中还有很多问题，例如上面例子实际上加载了全部的antd组件的样式（对前端性能是个隐患）。

## 优化方案：按需加载



#### 1. 安装antd

```javascript
npm install antd --save
```

#### 2. 安装（react-app-rewired

（react-app-rewired）一个对 create-react-app 进行自定义配置的社区解决方案

```javascript
yarn add react-app-rewired    /  cnpm install  react-app-rewired --save
```

#### 3. 修改package.jsonz中react-scripts 需改为react-app-rewired

```javascript
"scripts": {
  		"start": "react-app-rewired start",
  		"build": "react-app-rewired build",
  		"test": "react-app-rewired test --env=jsdom",
  		"eject": "react-app-rewired eject"
 }

```

4. 在项目根目录创建一个 config-overrides.js 配置文件

```javascript
const { injectBabelPlugin } = require('react-app-rewired');

module.exports = function override(config, env) {
  	 config = injectBabelPlugin(
    		   ['import', { libraryName: 'antd', libraryDirectory: 'es', style: 'css' }],
       	   config,
 	  );
  	 return config;
 };

```



5. 安装babel-plugin-import babel-plugin-import是一个用于按需加载组件代码和样式的 babel 插件

```javascript
yarn add babel-plugin-import   /  cnpm install babel-plugin-import --save

```

6. 然后移除前面在 src/App.css 里全量添加的

```javascript
@import '~antd/dist/antd.css'; 

```

7. 直接引入组件使用就会有对应的css：

```javascript
import { Button } from 'antd';

<Button type="primary">Primary</Button>

```

