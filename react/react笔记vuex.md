react笔记

## 注意点：

class是一个关键字， 类。 所以react 写class, 用classname   ，会自动编译替换class

点击方法：

```
 <button onClick = {this.sendData}>给父元素传值</button>
```



### 常用的插件： 

需要引入才能使用的：

````javascript
 路由五兄弟
 
import {BrowserRouter as Router, Link, Route, Redirect, Switch} from 'react-router-dom'


````

react-redux

npm install react-redux --save

### 初始配置  app页面

````javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

````



## 1.react简介：

简介：React 构建用户界面的javascript库，主要用于构建按ui界面。 instagram,2013年开源。

特点： 

*  声明式的设计
* 高效，采用虚拟DOM来实现DOM的渲染，最大限度的减少DOM的操作
* 灵活，跟其他库灵活搭配使用
* jsx, 俗称给你JS 里面写HTML, JavaSxript 语法的扩展。
* 组件化，模块化。代码容易复用，大型项目非常喜欢react.（2016年前，vue还没有火之前）
* 单项数据流/没有实现数据的双向绑定。  数据 --> 视图  --> 事件  --> 数据  

## 2 使用  引入react

### 2.1    CDN:      

只用于本地的学习和使用。 线上形目不能这样啊

可以通过 CDN 获得 React 和 ReactDOM 的 UMD 版本。

```javascript
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

### 2.2    脚手架

cnpm install -g create-React-app

````javascript

# 全局安装"create-react-app"架构
$ npm install -g create-react-app
 
# 创建脚手架项目
$ create-react-app my-app
 
# 进入项目目录
$ cd my-app
 
# 启动项目
$ npm start

http://localhost:3000/

执行npm start 时， 会自动编译dom，插入到src中的index.html，因为浏览器才不管你用了什么插件，他只会显示解析html正常的dom。

````

## 3. npm  start 发生了什么 代码原理

```javascript

入口文件:
1.网页入口文件放在 dist/index.html
2. react入口文件放在 src/index.js

在package.json的script中新增命令
"scripts": {
    "dev": "cross-env NODE=dev"
}



$ npm run build
# 等同于执行
$ node build.js

npm start是npm run start  简写形式

也就是说npm start=  node start.js 执行文件
npm run 查看当前项目的所有的


https://blog.csdn.net/cuipengchong/article/details/73044737?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522159479718919724811836533%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=159479718919724811836533&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v3-1-73044737.pc_ecpm_v3_pc_rank_v3&utm_term=npm%E8%84%9A%E6%9C%AC+npm+scripts
```

## 

````javascript

npm脚本 npm scripts
概念： npm脚本指的是package.json中的scripts字段
npm允许在package.json文件里面，使用scripts字段定义脚本命令。
就像 node 中执行1.js 可以写成 node 1  一样

"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },

scripts:{
"build":'node build.js'
}



````

----------------------分割线--------------------------

https://blog.csdn.net/qq_39956624/article/details/89352115?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522159479854019195264540861%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=159479854019195264540861&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v3-1-89352115.pc_ecpm_v3_pc_rank_v3&utm_term=react-scripts+start

在命令窗口输入的是npm start，而start调用的是

```
 package.json 中的
 
 "start": "react-scripts start",
```

 代码会找到 node_modules里面的react-scripts 插件。查找 bin 文件 点开bin\react-scripts.js文件内容

```
 .concat(require.resolve('../scripts/' + script))
 从上面这话可以看出调用start时需要调用scripts/start.js，点开该文件：
```

1. 打开config/paths.js，发现其实里面好多默认的配置都是写在该文件，可以通过修改改文件来实现自己文件的存放配置

2. 点开webpack.config.dev.js，也会发现大量是曾相识的代码：

3. 所以说我们以前通过手动配置的webpack.config.js的内容，react-scripts都已经帮我们做了，大大方便了我们的使用。

----------------------分割线--------------------------

npm的原理

npm 脚本的原理非常简单。每当执行npm run，就会自动新建一个 Shell，在这个 Shell 里面执行指定的脚本命令。因此，只要是 Shell（一般是 Bash）可以运行的命令，就可以写在 npm 脚本里面。

比较特别的是，npm run新建的这个 Shell，会将当前目录的node_modules/.bin子目录加入PATH变量，执行结束后，再将PATH变量恢复原样。

这意味着，当前目录的node_modules/.bin子目录里面的所有脚本，都可以直接用脚本名调用，而不必加上路径。比如，当前项目的依赖里面有 Mocha，只要直接写mocha test就可以了。

例如

"test": "mocha test"
1
而不用写成下面这样。

"test": "./node_modules/.bin/mocha test"


npm传参

向 npm 脚本传入参数，要使用–标明。

"lint": "jshint **.js"
1
向上面的npm run lint命令传入参数，必须写成下面这样。

$ npm run lint --  --reporter checkstyle > checkstyle.xml


```
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }

里面是一个个键值对，eject对应react-scripts eject，

当我们执行 npm eject的命令是，npm会找到 package.json中的scripts对象中eject对相应值，然后在执行。

```



### react文档结构

```javascript
myreact 

 
 |--node_modules   项目依赖包
 |-- public       公共开放资源  静态资源
 |     |--favicon.ico 
 |     | --index.html      相当于vue的 id ='app',等待放置编译好的dom
 |     | --logo.png         react图表
 |     | --mainifest.json  chrome扩展文件
 |     | --robots.txt       告诉爬虫，不要爬我的网页。一般没用。
 |
 |-- src
 |     |--App.css
 |     | --APP.js    app组件
 |     | --App.test.js
 |     | --index.css
 |     | --index.js   入口文件
 |     | --logo.svg
 |     | --servceWorker.js
 |     | --setupTests.js
 |
 | --.gittignore    git 忽略配置文件
 | --package.json    包配置信息
 | --package-lock.json  包配置信息版本固定
 | --README.md         文档说明   
 
 
webpack.config.js -  node_modules 


```

### 关于import...form...

index.js主文件为例

````javascript
import '../gen'  // 不支持根目录下的相对引入文件

import './1.js'
// require ('./1.js')  这两种引入方式，都可以打包进去。

自己的静态图片，官方希望你都放在src中，不要访问外边的资源。img js 新建目录存放。

````



## 4 react 组件原理

这是一个组件

App.js

```javascript
function App() {
  return (
      
    <div className="App">
        我是内容
    </div>

  );
}
```

这是

index.js   引用的页面

```javascript
import App from './App';  1.引入


ReactDOM.render(  2.  调用一个方法
  // <React.StrictMode>  严格模式
    <App />,
  // </React.StrictMode>,
  document.getElementById('root')
);


```



### 测试1：函数式组件渲染

index.js

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

// ReactDOM.render(
//     <App />,
//   document.getElementById('root')
// );

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister(); //缓存

页面生成时间，1s刷线一次。
function clock(){
  let time = new Date().toLocaleTimeString();
let element = <div>{time}</div>;
let root =  document.getElementById('root');
ReactDOM.render(element,root);
}

setInterval(clock,1000 )

```

### 测试2：组件传参

````javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

function Clock(props) {
  console.log(props);  //2.props  { data1:4,data2:40 }传入的值，会放到形参中。
  return ( 
    <div > 
     {  props.data1}
      </div>
    )
  }

function run(){

  ReactDOM.render(
  <Clock data1 = { 4} data2 = { 40}/>, //1. 标签首位字母大写

document.getElementById('root')
  );
  
}
  setInterval(run, 1000)


  // let time = new Date().toLocaleTimeString(); 
  //不同点： props
````



## 5  Jsx 表达式

优点： 

* JSX执行更快，编辑为JavsScript 代码是进行优化。

* 类型更安全，编译过程如果出错就不能编译，及时发现错误。

* JSX编写模板更加简单快速（不要更vue比，当时VUE还没出来）

  

  注意点：*  

  1. jsx必须要有根节点
  2. 正常的普通HTML元素要小写，如果是大写，默认认为是组件。

  

  jsx表达式：

  1.  有HTML元素构成
  2. 中间使用变量 用 { } 
  3. {} 中可以使用表达式 可以使用 jsx对象，
  4. 属性和html内容一样都是用{} 来插入内容。
  5. {} 一个只能放一个表达式  但可以放入嵌套数据结构

  

  

  

{ } 

#### 1.里放置表达式

```javascript
案例1 ：
var msg = '姓名';
var time = '00:00'

var dom = (
         <div>
                <div> {msg + time}</div>
        </div>
 )

ReactDOM.render(
  dom,
  document.getElementById('root')
 )



```

#### 2.案例2 ：三元运算法 

{ } 里面可以放标签和单元判断

```javascrip
var msg = '发烧';
var dom = (
         <div>
              <div> {msg == '发烧'?  <button>隔离</button> :'没事啊'}</div>
        </div>
 )

ReactDOM.render(
  dom,
  document.getElementById('root')
 )



```

#### 3. 混搭

 {<button>插值中放入标签，三元判断等</button>}

````javascript

var element4 = '我是混搭';
or

var element4 =
    <div>
          <span> 我是模板混搭 <sapn/> 
     </div>


<div> {msg == '发烧'?  <button>隔离</button> :element4}</div>
   
  dom变成了什么：     
element4：  dom,在这里已经变成了 一个对象。有属性和  _proto_       
       
````

## 4 引入css

App.css

````javascript

.lyx{
  color: red;
}
````



#### import引入 css 文件

比如当前页 index.js 

```
直接引入
import './App.css';

注意点： 
<div> {msg == '发烧'?  <div className='lyx'>隔离</div> :'没事啊'}</div>
加clsss  写法注意 className，
测试： 直接写 calss='lyx' 也可以。但是浏览器里会提示错误。

```



#### 变量js方式 css

````javascript
let  styledemo = {
  background:"skyblue",
  borderBottom:"4px solid red",  //需要驼峰
    "fontsize":'40px'    //要么加引号，不用驼峰
}

let element = (
<div>
  <h1 style = { styledemo} >我是 react style 的jsx变量写法</h1>
</div>
)


ReactDOM.render(
  element,
  document.getElementById('root')
 )

* 不能写行内样式，报错
````

  添加 自定义 class

````javascript

let classstr = 'redbg'

let element = (
<div>
  <h1 style = { styledemo} className = {'abc '+ classstr}>我是 react style 的jsx变量写法</h1>
</div>
)

变量类名 和自定义类名， abc 字符串类型，记得一定留出空格。否则编译出来会合并
className = {'abc '+ classstr} 


````

#### 1. 同时添加多个class

jsx标签中，不能加多个class, 需要处理一下，把class合并在写入。

````javascript
let classstr = ["redbg","redbg2"].join(" ") //合并字符串当成一个变量放入插值中

let element = (
<div>
  <h1 style = { styledemo} className = {classstr}>我是 react style 的jsx变量写法</h1>
</div>
)
````



## 5. jsx中加注释

````javascript
let element = (
<div>
  {/* jsx的注释写法*/}
  <h1 style = { styledemo} className = {classstr}>我是 react style </h1>
</div>
)
````



## 6. 组件的两种方式

### 6.1编程式  函数里（静态组件）

````javascript

function Childdom(){
  let title = <h2> 我是副标题</h2>
  let weather = '下雨'
//条件判断
 let isgo = weather === '下雨' ? "下雨不出门" : "不下雨了，不出门" 
  return(
  <div>  
    {title} 
    <span>
      天气怎么样:
      {isgo}
    </span>
    
  </div>
  )}

ReactDOM.render(
  <Childdom/>,
  document.getElementById('root')
 )


````

另一种传值形式，也是编程式 （组件传值）

````javascript
function Childdom(props){
  let title = <h2> 我是副标题</h2>
console.log(props);  // props接受传值
  return(
  <div>  
        {title} 
            <span>
              天气怎么样:
                  {props.weather}    // 使用传值
            </span>
    
  </div>
  )}
   
ReactDOM.render(
  <Childdom weather = '来自组件标签'/>,   //标签传值

  document.getElementById('root')
 )
````



### 6.2 类组件 class声明(动态组件)

index.js

````javascript

class HelloWorld extends React.Component{
 render() {                //render这个名字不能动。不是随意取得。是一个规定的方法
      return(
        <div>  
        我是类组件定义
        </div>
      )
 }
}


ReactDOM.render(
  <HelloWorld/>,
  document.getElementById('root')
 )



````

### 组件 

类组件传参-见序号8

````javascript

  class Ant extends React.Component {
    constructor(props) {
      super(props)
    this.state = {}
    }
  
    render() {

      return ( 
        <div > 
          
        </div>
      )
    }

    onChange(page,pagesize){
     
    }
  }


export default Ant


````



### 6.3组件嵌套（复合组件）

````javascript

class Children extends React.Component{
  render() {               
       return(
         <div>  
     <div> 我是Children</div>


         </div>
       )
  }
 }

  class HelloWorld extends React.Component{
    render() {              
         return(
           <div>  
       <div> 我是HelloWorld</div>
          <Children/>    //helloworld组件中，引入children组件
           </div>
         )
    }
   }
   
   ReactDOM.render(
     <HelloWorld  weather = '出太阳'/>,
     document.getElementById('root')
    )
````

结论：两种组件适用场景

函数式： 如果静态，或者就 传一个值，使用函数式

类组件：有触发事件，交互和操作



## 7. 关键方法：ReactDOM.rende

````javascript
ReactDOM.render(组件， 挂载点root)

````

组件这一块，样式可以多种。

### 第一种 ：  function ( )  函数形式

````javascript
function Childdom(){
  let title = <h2> 我是副标题</h2>
  let weather = '下雨'
//条件判断
 let isgo = weather === '下雨' ? "下雨不出门" : "不下雨了，不出门" 
  return(
  <div>  
    {title} 
    <span>
      天气怎么样:
      {isgo}
    </span>
    
  </div>
  )}

ReactDOM.render(
  <Childdom/>,
  document.getElementById('root')
 )

````

### 第二种 ：   dom形式

````javascript
其实实质一样，和return（） 函数式一样。

let element = (
<div>
  <h1 style = { styledemo} >我是 react style 的jsx变量写法</h1>
</div>
)


ReactDOM.render(
  element,
  document.getElementById('root')
 )
````

8 传值

```javascript
function Childdom(props){
  let title = <h2> 我是副标题</h2>
console.log(props);  // props接受传值
  return(
  <div>  
        {title} 
            <span>
              天气怎么样:
                  {props.weather}    // 使用传值
            </span>
    
  </div>
  )}
   
ReactDOM.render(
  <Childdom weather = '来自组件标签'/>,   //标签传值

  document.getElementById('root')
 )
```



## 8 传值（类组件传参）

### 8.1 自己的标签 ——> 传向自己的组件

````javascript
class Children extends React.Component{
  render() {     
    console.log(this);   //这里的this指的是Children组件 this里propos里有标签传值
       return(
         <div>  
     <div> 我是Children</div>


         </div>
       )
  }
 }

  class HelloWorld extends React.Component{
    render() {       
      console.log(this);   //这里的this指的是HelloWorld组件 this里propos里有标签传值
         return(
           <div>  
       <div> 我是HelloWorld</div>
          <Children name = '我是children的数据' />   
           </div>
         )
    }
   }
   
   ReactDOM.render(
     <HelloWorld  weather = '我是父组件穿的值'/>,
     document.getElementById('root')
    )
````

### 8.2 父组件 标签的数据--> 子组件  传递

  ````javascript

class Children extends React.Component{
  render() {     
    // console.log(this);   //这里的this指的是Children组件 this里propos里有标签传值
       return(
         <div>  
     <div> 我是Children</div>


         </div>
       )
  }
 }

  class HelloWorld extends React.Component{
    render() {       
      console.log(this);   //这里的this指的是HelloWorld组件 this里propos里有标签传值
         return(
           <div>  
       <div> 我是HelloWorld</div>
          <Children name = '我是children的数据' weather = {this.props.weather}/>   
           </div>
         )
    }
   }
   
   ReactDOM.render(
     <HelloWorld  weather = '我是父组件穿的值'/>,
     document.getElementById('root')
    )
  ````

## 9 react状态 管理（修改数据）

### 9.1 引入例子

````javascript

class Clock extends React.Component {
  constructor(props) {
    super(props)
  this.state = {
    time: new Date().toLocaleTimeString()
    }}

  render() {
 // console.log(1);  变了
    return ( 
      <div >
    <h1> 当前时间： {this.state.time}</h1>
      </div>
    )
  }
}

setInterval(()=>{
  // console.log(0);  变了
ReactDOM.render(
  <Clock/> ,
  document.getElementById('root')
);

},1000)

计时器1s渲染一次，我们发现页面没动。手动刷新才会变。
通过打印我们发现，render, 计时器都在变，就是页面不变。
原因是： render方法 每隔1s渲染， <Clock/> 直接加载缓存。所以没变。
````

既然render变了，那就直接修改state.time的值。

````javascript
 做如下修改
render() {
  // console.log(0);
              this.state.time = new Date().toLocaleTimeString()
    return ( 
      <div >
                 <h1> 当前时间： {this.state.time}</h1>
      </div>
    )
  }
  
  保存后，页面动了。 
````

但是这不是官方推荐的方法。

### 9.2 正确修改方法    setState(  )

````javascript

class Clock extends React.Component {
    平级1
  constructor(props) {
    super(props)
      this.state = {
    time: new Date().toLocaleTimeString()
    }}
  平级2
  render() {
    return ( 
      <div >
                 <h1> 当前时间： {this.state.time}</h1>
      </div>
    )
  }
    平级3
   componentDidMount(){   componentDidMount是声明周期函数，加载完页面开始执行。
    setInterval(() => {
      
      this.setState({
        time : new Date().toLocaleTimeString()
      })
    }, 1000);
   }
}

渲染函数
ReactDOM.render(
  <Clock/> ,
  document.getElementById('root')
);


1.采用官方方法的作用： 修改数据，并自动渲染页面；
2. setstate方法，修改数据后，不会立即更改dom，而是等函数执行完了以后，统一对比虚拟dom,再做修改，提升性能。 小程序也是借鉴这样。
````

总结： react 类组件中，自己的state数据，和点击事件，和渲染dom,都放到自己的内部，this下挂载。

### 9.3 案例：

####  实现两个按钮接环内容

````javascript
import React from 'react';
import ReactDOM from 'react-dom';

class Clock extends React.Component {
  constructor(props) {
    super(props)
  this.state = {
    c1:"content active",
    c2:"content "

    }
    this.clickEvent = this.clickEvent.bind(this)// 把方法挂载到this组件下

  }

      clickEvent(e){
        console.log(this);
          // console.log(e.target.dataset);
          // console.log(e.target.dataset.index);

         let index = e.target.dataset.index
         if(index == '1'){
           this.setState({
            c1:"content active",
            c2:"content "
           })
         }else{
          this.setState({
            c1:"content ",
            c2:"content  active"
           })
         }
      }

  render() {
    return ( 
      <div >
             <button data-index = '1' onClick = {this. clickEvent }>内容一</button>  
             <button data-index = '2' onClick = {this. clickEvent }>内容二</button>  
            
             <div className = {this.state.c1}>
                          <h1>内容一</h1>   
             </div>
             <div className = {this.state.c2}>
                          <h1>内容二</h1>   
             </div>

      </div>
    )
  }
  
}

ReactDOM.render(
  <Clock/> ,
  document.getElementById('root')
);

案例里：用到了几个点
e 事件对象
DOM data自定义属性和使用
bing(this) 改变this指向

````

## 10  传值

### 10.1  父传子

父传子数据，单向流动，不能子传父。 props的传值，可以是任意的类型。

props可以设置默认值。 

HelloMessage.dafaultProps = { name:'tom' ,msg:'hellowlorld' }

注意：prop可以传递函数，可以传递父元素的函数。也就是说，可以修改父元素的state数据，从而道道传递 数据 的效果和目的。

````javascript
import React from 'react';
import ReactDOM from 'react-dom';

class Clock extends React.Component {
  constructor(props) {
    super(props)
  this.state = {
    isshow:true

    }
      this.changeshow = this.changeshow.bind(this)
  }

  changeshow(){
    this.setState({
      isshow:!this.state.isshow
    })
    
         }


  render() {
    return ( 
      <div >
        <button onClick = {this.changeshow}>控制子元素显示</button>
            <Children  isactive = {this.state.isshow}/>

      </div>
    )
  }
  
}

class Children extends React.Component {
  constructor(props) {
    super(props)
  this.state = {
    }

  }

      render() {
        let strclass = null;

        if(this.props.isactive){
          
          strclass = 'active'
        }else{
      
          strclass = ""
        }

    return ( 
      <div >
        <span className = {'content '+ strclass}>i is children</span>
      </div>
    )
  }
  
}

ReactDOM.render(
  <Clock/> ,
  document.getElementById('root')
);

总结: 父元素states准备一个变量，在自己函数内，子组件标签，输入值， 子组件接受props接受使用。
````

### 10 2 子传父

方法： 调用父元素的函数，从而操作元素的数据。

````javascript
import React from 'react';
import ReactDOM from 'react-dom';




class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
    childData:null  //默认是null页面不会显示，只有 有数据才会显示
   }
    
  }


  render() {
    return ( 
      <div >
      <h1>子元素传递给复原的数据 {this.state.childData} </h1>
      <Children setChildDate = {this.setChildDate} />       //1. 变量也可以是个方法

      </div>
    )
  }
  setChildDate = (a)=>{  //3.传递形参，进行修改
    this.setState({
      childData:a
    })
  }
}

class Children extends React.Component {
  constructor(props) {
    super(props)
  this.state = {
    msg:'helloworld'
    }
  }

  sendData = ()=>{
      this.props.setChildDate(this.state.msg) // 2. 你要记住，标签传参，实例中props中就会有值。
  }
      render() {
        return ( 
          <div >
            <button onClick = {this.sendData}>给父元素传值</button>
          </div>
        )
  }
}
  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );

简写形式： 既然children标签传入， children的props中就会挂载。那么就可以这样写：
 <button onClick = {()=> {this.props.setChildDate('我是子组件调用props')}}>给父元素传值</button> ，这样也是可以调用的。   匿名的箭头函数，this.不变。

````

## 11  reach 事件语法

##### 

#### 特点： 

1. 事件的 click 写法，驼峰命名法。2. { } 传入一个函数，而不是一个字符串.

````javascript
<button onClick = {this.sendData}>给父元素传值</button>
````

#### 处理过的事件对象e 和 阻止默认

````javascript
import React from 'react';
import ReactDOM from 'react-dom';


class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
 
   }
  }
  render() {
    return ( 
      <div >
   <div onClick = { this.parentEvent } data-index = 'lyx'>
     查看事件对象e
   </div>
      </div>
    )
  }
  parentEvent = (e)=>{
    console.log( e) //注意：这个事件都想是react 处理过的。如果想拿到具体值，直接输出 e.target.dataset.index
  }
}
  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );

````

阻止默认

````javascript
  组件： 
form 有默认提交事件，同步的。如果想自定义ajax异步请求，就阻止默认。
render() {
    return ( 
      <div >
             <form action="https://www.baidu.com" method="get">
                     <button onClick = {this.parentEvent}>提交</button>
           </form>
      </div>
    )
  }
  
  
  方法1：
    parentEvent = (e)=>{
    console.log(e ) //注意：想知道e中有什么方法，打印出来一个一个查一下。 
    e.preventDefault()
  }
  方法2
  form中的提交按钮，submit修改为button , 不设置默认submit.
  <button onClick = {this.parentEvent} type = 'submit'>提交</button>
````

#### 传参，同时保留事件对象



````javascript
  render() {
    return ( 
      <div >
           <form action="https://www.baidu.com" method="get">
          <button onClick = {(e)=>{this.parentEvent(e, "0")}} type = 'button'>提交</button>
           </form>
      </div>
    )
  }
  parentEvent = (e,a)=>{
    console.log(e ,a) //注意：想知道e中有什么方法，打印出来一个一个查一下。 
    // e.preventDefault()
  }
````

#### 注意：

````javascript
<button onClick = {()=>{this.parentEvent("0")}} type = 'button'>提交

这样的话，传值，会把e替换。
````

#### 不适用箭头函数传递多个参数

  箭头函数与function函数的区别,就是this. 所以bind,修改一下this.指向。

function, 内部的this，就是它自己，谁调用，指向谁。

````javascript
使用箭头函数
<button onClick = {()=>{this.parentEvent("0")}} type = 'button'>提交</button>
不适用箭头函数
 <button onClick = {function(e){this.parentEvent('msg:helloworld',e)}.bind(this)} type = 'button'>提交</button>


 parentEvent = (e,a)=>{
    console.log(e ,a)  //形参，按位置传递 
  
  }
````



## 12  条件渲染

React 中条件渲染即和JavaScript 中，条件运算，如if else 三元运算符等等。

1 直接通过条件渲染你返回要渲染的jsx对象。

2 通过条件运算得出jsx对象，在将jsx对象渲染到模板中。

#### 第一种

````javascript
import React from 'react';
import ReactDOM from 'react-dom';

function User(props){
  return ( <h1>我登陆了</h1>)
}

function UserNologin(props){
  return ( <h1>请登录</h1>)
}

class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
      islogin:false
   }
  }
  render() {
    if(this.state.islogin){
      return(<User></User>)
    }else{
      return(<UserNologin></UserNologin>)
    }
  }
}

  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );
通过控制islogin， 达到页面变化。

````

#### 第二种

````javascript
import React from 'react';
import ReactDOM from 'react-dom';



function User(props){
  return ( <h1>我登陆了</h1>)
}

function UserNologin(props){
  return ( <h1>请登录</h1>)
}

class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
      islogin:false
   }
  }
  render() {
    let element = null

    if(this.state.islogin){
      element =( <User></User> )
    }else{
      element =  (<UserNologin></UserNologin>)
    }

      return(  
        <div> 
          <div>这是头部</div>
            {element}
        <div>这是尾部</div>
        </div>
      )
  }
}



  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );

//可以发现， react 就是你想要什么样的逻辑，自己动手。
````

#### 第三种： 三元运算符形式

````javascript
render() {
   
      return(  
        <div> 
          <div>这是头部</div>
            {this.state.islogin ?( <User></User> ):  (<UserNologin></UserNologin>)}
        <div>这是尾部</div>
        </div>
      )
  }
````

## 13 列表渲染

将列表内容拼装成数组放置到模板中。

将数据封装成数组的JSX对象。

````javascript
import React from 'react';
import ReactDOM from 'react-dom';



let arr = ['小明','小黑','小白']

class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
      islogin:true
   }
  }
          render() {
              return(  
                <div> 
                    <ul>
                          {arr}
                    </ul>
                </div>
              )
          }
}

  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );


渲染结果：
<ul>
  小明
小黑
小白
</ul>
````

### 改造：

````javascript
let arr = ['小明','小黑','小白']

我们设置一个jsx数组

let arrhtml = [<li>小明</li>,<li>小黑</li>,<li>小白</li>]

               
  render() {
              return(  
                <div> 
                    <ul>
                          {arrhtml}
                    </ul>
                </div>
              )
          }
        
渲染结果： 完美
<ul><li>小明</li><li>小黑</li><li>小白</li></ul>
      
````

### 列表循环jsx。

````javascript
import React from 'react';
import ReactDOM from 'react-dom';


class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
     listarr : [
       {
          title:'第一个标题1',
          cont:'我是内容1'
       },
       {
          title:'第一个标题2',
          cont:'我是内容2'
       }
     ]
   }
  }
          render() {
            let listArr = []
            console.log(0);
            for(let i = 0 ;i < this.state.listarr.length;i++){
      
              var  item =  (
                <li>
                  <h3>{this.state.listarr[i].title}</h3>
                   <p>{this.state.listarr[i].cont}</p>
                </li>
              )
              listArr.push(item) 
            }
      
              return(  
                <div> 
                    <ul>
                          {listArr}
                    </ul>
                </div>
              )
          }
}



  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );

````

### 代码简化 map循环 

使用数组的map方法，对每一项数据按照JSX的形式加工，最终得到，每一项都是JSX对象的数组，在将数组渲染到模板中去。

````javascript
  render() {
            let listArr = this.state.listarr.map((itme,index)=>{
              return(
             <div key = {index} className = {'item'+index}>
                    <li>{itme.title}</li>
                    <p>{itme.cont}</p>
             </div>
            
              )
            })
              return(  
                <div> 
                    <ul>
                          {listArr}
                    </ul>
                </div>
              )
          }
````

## 14 肺炎列表渲染案例

总结： render里面可以写js逻辑，完全就是原生js写的。

这个暂用：



````javascrpt
import React from 'react';
import ReactDOM from 'react-dom';

var data = require('./1.json')
console.log(data);

class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
     listarr : [
       {
          title:'第一个标题1',
          cont:'我是内容1'
       },
       {
          title:'第一个标题2',
          cont:'我是内容2'
       }
     ]
   }
  }
          render() {
            let listArr = this.state.listarr.map((itme,index)=>{
              return(
             <div key = {index} className = {'item'+index}>
                    <li>{itme.title}</li>
                    <p>{itme.cont}</p>
             </div>
            
              )
            })
            
              return(  
                <div> 
                    <ul>
                          {listArr}
                    </ul>
                </div>
              )
          }
}



  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );

````

![1594992881748](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1594992881748.png)



## 15 生命周期函数

https://blog.csdn.net/qq_38719039/article/details/82378434

![img](https://upload-images.jianshu.io/upload_images/13691847-eba0fcccaf3b97f0.png?imageMogr2/auto-orient/strip|imageView2/2/w/807/format/webp)

生命周期：  针对组件总渲染到销毁的过程。期间有可以调用的函数，又叫钩子函数

生命周期的3个状态。

Mounting： 将组件插入到dom中。

Updating: 将数据更新到dom中。

Unmounting: 将组件移除Dom中。



生命周期中的钩子函数（方法，事件）

componentWillMount： 组件将要渲染                              -> AJAX，添加动画前的类

componentDidMount ： 组件渲染完毕                                ->    添加动画  添加echart 就在这里 获取windown

compontWillReceiveProps：组件将要接受props数据       ->查看props的数据是什么

componentWillReceiveProps: 组件接收到新的state或者props   ->判断是否更新。 返回布尔值。

CompontWillUpdate : 组件将要更新

componentDidUpdate ：组件已经更新

componentWillUnmount : 组件 将要卸载

  // 已经更正

### 1.constructor(props, context)

- 构造函数，在创建组件的时候调用一次。

### 2.componentWillMount()

- 在组件render之前立即调用

`Tip1`: 不建议在此请求数据，由于请求数据接口一般都是异步，这时候render已经被执行，建议在componentDidMount 数据

`Tip2`: 如果在服务端渲染，该钩子函数将被调用两次，一次服务端，一次浏览器端，而componentDidMount函数只会在浏览器端请求一次

`Tip3`: 在taro构建的小程序里对应的生命周期是 onLoad。

### 3..componentDidMount()

- 所有的组件（包括子组件）在render执行完之后立即调用，并且只会被调用一次。

`Tip`: 建议在此请求数据

### 4. componentWillReceiveProps(nextProps)

- 在props被改变时被触发，初始化render时不调用。
- 旧的属性还是可以通过this.props来获取，在这里通过调用this.setState()来更新你的组件状态。

`Tip1`: 某些情况下，props没变也会触发该钩子函数，需要在方法里手动判断一下this.props和nextProps是否相同，不相同了才执行我的更新方法。

`Tip2`：该函数一般用来更新依赖props的状态

### 5. shouldComponentUpdate(nextProps, nextState)

- 发生重渲染时，在render()函数调用前被调用的函数，当函数返回false时候，阻止接下来的render()函数的调用，阻止组件重渲染，而返回true时，组件照常重渲染。
- 该方法并不会在初始化渲染或当使用forceUpdate()时被调用。

### 6.componentWillUpdate(nextProps, nextState)

- shouldComponentUpdate返回true或者调用forceUpdate之后，componentWillUpdate会被调用。

### 7. getSnapshotBeforeUpdate(prevProps, prevState)

- 该函数在最新的渲染输出提交给DOM前将会立即调用。它让你的组件能在当前的值可能要改变前获得它们。这一生命周期返回的任何值将会 作为参数被传递给componentDidUpdate()。

### 8. componentDidUpdate(prevProps, prevState)

- 除了首次render之后调用componentDidMount，其它render结束之后都是调用componentDidUpdate。

### 9.componentWillUnmount()

- 在组件被卸载和销毁之前立刻调用。可以在该方法里处理任何必要的清理工作，例如解绑定时器，取消网络请求，清理任何在componentDidMount环节创建的DOM元素。

### 10.componentDidCatch(error, info)

- 该函数称为错误边界，捕捉发生在子组件树中任意地方的JavaScript错误，打印错误日志，并且显示回退的用户界面。

`Tip`：错误边界只捕捉树中发生在它们之下组件里的错误。一个错误边界并不能捕捉它自己内部的错误。

### 11.render()

- render是一个React组件所必不可少的核心函数（上面的其它函数都不是必须的）。

`Tip`：记住，不要在render里面修改state。

### 12.React组件更新路径

在线测试：http://wximg.gtimg.com/shake_tv/test/lifeCycle2113.html

### 钩子函数位置 ( 完整code)

````javascript
import React from 'react';
import ReactDOM from 'react-dom';



class Clock extends React.Component {
  constructor(props) {
    super(props)
      this.state = {
        msg:'hello world'
      }
  }


// componentWillMount   组件将要渲染
componentWillMount(){
  console.log(' CompontWillMount： 组件将要渲染')
}

// CompontDidMount： 组件渲染完毕
CompontDidMount(){
  console.log(' CompontDidMount： 组件渲染完毕')
}
// compontWillReceiveProps：组件将要接受props数据
compontWillReceiveProps(){
  console.log(' compontWillReceiveProps：组件将要接受props数据')
}
// componentWillReceiveProps : 组件接收到新的state或者props，判断是否更新。 返回布尔值。
componentWillReceiveProps(){
  console.log(' componentWillReceiveProps: 组件接收到新的state或者props')
}

// CompontWillUpdate: 组件将要更新
CompontWillUpdate(){
  console.log(' CompontWillUpdate: 组件将要更新')
}

// componentDidUpdate组件已经更新

componentDidUpdate(){
  console.log(' ComponentDidUpdate：组件已经更新')
}

// componentWillUnmount : 组件 将要卸载

componentWillUnmount(){
  console.log(' componentWillUnmount : 组件 将要卸载')
}

          render(){

              return(  
                <div> 
                  
                </div>
              )
          }
}



  ReactDOM.render(
    <Clock/>,
    document.getElementById('root')
  );

总结： 钩子函数在构造函数内，
````

测试：使用上面的code， 测试，页面打开的时候：显示  CompontWillMount：组件将要渲染

 点击修改数据的时候： ComponentDidUpdate：组件已经更新。  其他的等待测试。

```javascrpt


```





### 补充： 组件的成员和他们的this

```javascript
import React from 'react';
import ReactDOM from 'react-dom';



class Clock extends React.Component {

// ----------------------分割线----------------------------------------------
  constructor(props) {
    super(props)
      this.state = {
        msg:'hello world'
      }
      console.log(this);// this指向实例
      this.clickEvent = this.clickEvent.bind(this)// 把方法挂载到this组件下
  }


// ----------------------分割线----------------------------------------------

          render(){
            console.log(this); // this指向实例
              return(  
                <div> 
                  {/* <button onClick = {this.clickEvent}>点击修改数据</button> */}
                  <button onClick = {this.clickEvent.bind(this)}>点击修改数据</button>
                  <span>{this.state.msg}</span>
                </div>)}

// ----------------------分割线----------------------------------------------
            clickEvent(e){
//没有bing，this= undefind ;加上bing现在this已经指向实例.才能使用实例上的方法。this.setstate
           console.log(this); 
              // this.setState({
              //   msg:'修改内容'
              // })
            }
// ----------------------分割线----------------------------------------------

} // 组件的下括号

//  上图表明： 组建中三个部分： constructor   render   dom的clickEvent  三个是并列。
// 正由于是并列的，所以this不统一。  
//  所以只要保证this是统一实例。 button可以这两中写法。看上图

  ReactDOM.render(
    <Clock/>,
    document.getElementById('root')
  );
```





### 案例： 疫情 中国地图 引入echart

````javascript

npm install echarts

import React from 'react';
import ReactDOM from 'react-dom'; //

var echarts = require('echarts');//该中引入方式默认实在node_modules 中 npm安装



class Clock extends React.Component {
// -----------------分割线---------------------------
  constructor(props) {
    super(props)
      this.state = {
        msg:'hello world',
        my_series_data:[5, 20, 36, 10],
        my_xAxis_data:["衬衫", "羊毛衫", "雪纺衫", "没有裤子"]
      }
  }
// -----------------分割线---------------------------
      componentDidMount() {
        console.log(this); //指向实例
        // 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));
        // 绘制图表
        let shuju ={
          title: { text: 'ECharts 入门示例' },
          tooltip: {},
          xAxis: {
              data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
          },
          yAxis: {},
          series: [{
              name: '销量',
              type: 'bar',
              data: [5, 20, 36, 10, 10, 20]
          }]
      }
          //  拦截原始数据，用自己的数据替换一下
          console.log(shuju);
           shuju.series[0].data = this.state.my_series_data
           shuju.xAxis.data = this.state.my_xAxis_data

        myChart.setOption(shuju);  //渲染图表

    }
// -----------------分割线---------------------------
          render(){
              return(  
                <div className="myecahrt"> 
                        <h1>我的creact 图表</h1>
                        <div id="main" style={{ width: 400, height: 400 }}></div>
                </div>)
                }
// -----------------分割线---------------------------
} 


  ReactDOM.render(
    <Clock/>,
    document.getElementById('root')
  );

  // 总结： npm 引入 js  ；data中准备好自己的数据； render中准备好挂载点，
  // ；钩子函数，组件dom渲染上后，寻找dom，初始化echart方法，在渲染前替换自己的的数据。
 

````

### 引入echar map地图

```
import React from 'react';
import ReactDOM from 'react-dom'; 


import echarts from 'echarts'

import 'echarts/map/js/china';

  // require ('echarts/map/js/china')


// import ('echarts/map/js/china');  采用该种方法引入 报错 如下：
// Expected an assignment or function call and instead 
// saw an expression  no-unused-expressions

 class App extends React.Component {
  // export class App extends Component {
    constructor(props) {
        super(props);
        this.state = {
        
            data:[
                {
                    name: "南海诸岛",
                    value: 0
                },
                {
                    name: '北京',
                    value: 20
                },
                {
                    name: '天津',
                    value: 30
                },
                {
                    name: '上海',
                    value: 229
                },
                {
                    name: '重庆',
                    value: 59
                },
                {
                    name: '河北',
                    value: 190
                },
                {
                    name: '河南',
                    value: 300
                },
                {
                    name: '云南',
                    value: 20
                },
                {
                    name: '辽宁',
                    value: 40
                },
                {
                    name: '黑龙江',
                    value: 37
                },
                {
                    name: '湖南',
                    value: 180
                },
                {
                    name: '安徽',
                    value: 0
                },
                {
                    name: '山东',
                    value: 67
                },
                {
                    name: '新疆',
                    value: 10
                },
                {
                    name: '江苏',
                    value: 0
                },
                {
                    name: '浙江',
                    value: 0
                },
                {
                    name: '江西',
                    value: 0
                },
                {
                    name: '湖北',
                    value: 0
                },
                {
                    name: '广西',
                    value: 0
                },
                {
                    name: '甘肃',
                    value: 0
                },
                {
                    name: '山西',
                    value: 0
                },
                {
                    name: '内蒙古',
                    value: 89
                },
                {
                    name: '陕西',
                    value: 0
                },
                {
                    name: '吉林',
                    value: 0
                },
                {
                    name: '福建',
                    value: 66
                },
                {
                    name: '贵州',
                    value: 0
                },
                {
                    name: '广东',
                    value: 330
                },
                {
                    name: '青海',
                    value: 0
                },
                {
                    name: '西藏',
                    value: 74
                },
                {
                    name: '四川',
                    value: 601
                },
                {
                    name: '宁夏',
                    value: 0
                },
                {
                    name: '海南',
                    value: 45
                },
                {
                    name: '台湾',
                    value: 23
                },
                {
                    name: '香港',
                    value: 0
                },
                {
                    name: '澳门',
                    value: 0
                }
            ]
       

        }
    }

    componentDidMount(){
        this.initMap();
    }
    
    //初始化地图

    initMap = () => {
        let myChart = echarts.init(document.getElementById('myMap'));
        let option = {
            tooltip: {
                formatter: function (e , t, n) {
                    return e.seriesName + "<br />" + e.name + "：" + e.value
                }
            },
            visualMap: {
                min: 0,
                max: 1000,
                right: 26,
                bottom: 40,
                showLabel: !0,
                pieces: [{
                    gt: 500,
                    label: "500家以上",
                    color: "#ED5351"
                }, {
                    gte: 200,
                    lte: 500,
                    label: "201-500家",
                    color: "#3B5A97"
                }, {
                    gte: 100,
                    lt: 200,
                    label: "101-200家",
                    color: "#59D9A5"
                }, {
                    gt: 51,
                    lte: 100,
                    label: "51-100家",
                    color: "#F6C021"
                }, {
                    label: "1-50家",
                    gt: 0,
                    lte: 50,
                    color: "#6DCAEC"
                }
                ],
                show: !0
            },
            geo: {
                map: "china",
                roam: !1,
                scaleLimit: {
                    min: 1,
                    max: 2
                },
                zoom: 1.13,
                layoutCenter: ['30%', '30%'],                //地图中心在屏幕中的位置
                label: {
                    normal: {
                        show: !0,
                        fontSize: "14",
                        color: "rgba(0,0,0,0.7)"
                    }
                },
                itemStyle: {
                    normal: {
                        borderColor: "rgba(0, 0, 0, 0.2)"
                    },
                    emphasis: {
                        areaColor: "#F5DEB3",
                        shadowOffsetX: 0,
                        shadowOffsetY: 0,
                        borderWidth: 0
                    }
                }
            },
            series: [{
                name: "客户统计",
                type: "map",
                geoIndex: 0,
                data: this.state.data,
                areaColor: '#0FB8F0'
            }]
        };
        myChart.setOption(option);
        window.addEventListener("resize", function () {
            myChart.resize();
        });
    }
  
      render(){
        return (
            <div className="map">
                <div id="myMap" style = {{"height":"800px"}} ></div>
            </div>
        )
    }
}



    ReactDOM.render(
      <App/>,
      document.getElementById('root')
    );



```



## 16 表单和图表 seach案例



涉及点： 父子传值， 常规dom渲染理解为jsx对象，map循环，

子页面的绑定事件，模块导出。

index.js

````javascript
import React from 'react';
import ReactDOM from 'react-dom';


import Search from './component/search';

class Clock extends React.Component {

  constructor(props) {
    super(props)
   this.state = {
     listarr : [
       {
         id:1,
          title:'第一个标题1',
          cont:'我是内容1'
       },
       {
        id:2,
          title:'第一个标题2',
          cont:'我是内容2'
       }
     ]
   }
  }
          render() {
            let listArr = this.state.listarr.map((itme,index)=>{
              return(
             <div key = {index} className = {'item'+index}>
                    <li>{itme.title}</li>
                    <p>{itme.cont}</p>
             </div>
            
              )
            })
            
         

              return(  
          
                <div> 
                  <Search alldata = {this.state.listarr}></Search>
                    <ul>
                          {listArr}
                    </ul>
                </div>
              )}
}

  ReactDOM.render(
    <Clock/> ,
    document.getElementById('root')
  );
````



search.js页面

````javascript
import React from 'react';

class Search extends React.Component {

    constructor(props) {
      super(props)
     this.state = {
        value:undefined,
        result:":查询结果"
     }
    }
                render() {
                    return(   
                        <div className= 'search'> 
                              <input type="text" onKeyDown = {this.serchEvent.bind(this)}  placeholder='请输入' 
                            //   value = {this.state.value}
                            //   onChange = {this.chengeEvent.bind(this)}

                              />
                                    <div>
                                        <h2>查询结果</h2>
                                        <div>
                                            这是查询结果 search
                                            {this.state.result}
                                        </div>
                                    </div>
                         
                        </div>
                    )}

      serchEvent(e){
            // let a = this.props.alldata[e.target.value]
            if(e.keyCode === 13){
 
                if(this.props.alldata[e.target.value]){
                    this.setState({
                        result :(<h2>{this.props.alldata[e.target.value].cont}</h2> )
                    })
                }else{
                    this.setState({
                            result :(<h2>只有两条数据啊</h2> )
                  
                    })
                }  
            }
      }

      chengeEvent(e){

// console.log(e.target.value);
            this.setState({
                // value:e.target.value
            })
      }
    }
    
    export default Search;
````







## 17 React 的ajax案例

Ajax + React + axios + Express  案例

## 17-1  服务端

### 环境准备

````javascript
常规准备
1. npm init    生成package.son文件 记录以来信息
2. npm i webpack --save-dev   安装webpack  生成node_modules 打包依赖文件  18M大小
项目使用的插件和框架准备

3.npm install express --save      --save是保存版本信息。其中主要封装的是http。   
4.  npm install --global  n         odemon热加载


````

### 新建index.js

````javascript
// 0 安装 
// 1 引包
const express = require('express')  // 引包

const app = express() //调用
// app.get('/', (req, res) => res.send('Hello World!'))  //res.send 这里 变了

app.get('/', function(req, res){
        res.send('Hello World!')
})

  // 再写一个
app.get('/app', function(req, res){
        res.send('您好我是：app')
})

// app.listen(3000, () => console.log('running...'))
app.listen(3000, function(){
        console.log('running...')
})
````

### 启动服务： 

````javascrpt
cmd 命令行中输入： nodemon app.js 

ok项目启动 浏览器打开 
基本的服务搭建完成
````

### 项目使用的插件

axios  

```javascrpt
npm install axios --save

注意引入index.js
```

asynchronous 异步

疫情接口( 仅学习使用)

https://voice.baidu.com/newpneumonia/get?target=trend&isCaseIn=0&stage=publish&callback=jsonp_1595142630965_83751（jsonp格式转换json格式）

````javascript

app.get('/api', async function(req, res){
      //解决跨域问题
//   res.json({name:'lyx'})
let url = 'https://voice.baidu.com/newpneumonia/get?target=trend&isCaseIn=0&stage=publish&callback=jsonp_1595142630965_83751'
  let resdata = await axios.get(url)
        let data =resdata.data;
        // res.send(data)
       res.json(data) 
    
})

打开页面，可以看到数据
````







## 17-2  前端

1. 初始化react项目包

   包含操作： npm init    /npm webpack  / 外加两个文件夹/   md说明文档/    就是一个快捷操作

```javascrpt
 create-react-app reactapp
```

2.   axios  前端安装 axiox    都自己的node_modules

```javascrpt
npm install axios --save

注意引入app.js
const axios = require('axios')  
```

前端访问疫情接口： 

```
		  async	componentWillMount(){
				console.log(0)
				// axios.get()
let url = 'https://voice.baidu.com/newpneumonia/get?target=trend&isCaseIn=0&stage=publish&callback=jsonp_1595142630965_83751'
 let resdata = await axios.get(url)
 let data =resdata.data;
 console.log(data);
			          }
```





跨域： 解决

````javascript
 这就是搭建后台的原因：

async	 componentWillMount(){
        let url = 'http://localhost:4000/api'
         let resdata = await axios.get(url)
         let data_ = resdata.data.features

          this.setState({
            Newslistdata:data_
          })

        console.log('前台返回第一层数据',data_);	 
        }

````





页面结构

1. 这里的4个tab切换，不是路由，而是在主页面中引入了4个子页面。 放在主页面的cont中，flex横向排列。

   点击tab,控制父盒子的定位左侧移动。

   2.实现点击tab bar动画： state准备：tabIndex，条件渲染tab，tab 设置点击事件，this.setState({}）方式修改tabIndex，dom会根据数据变化，自动重新渲染。 4个tab移动意识一样。

   3. new页面的数据，为自己请求的数据。

   4.  图片的引入和使用： 引入后的变量  ：  src = {变量}

      import Bannerimg from './assets/img/newbanner.jpg';

      <img src={Bannerimg} alt="图片" className = "newimg" />

````javasccript
import React from 'react';
import './assets/css/styls.css';

import NewsCom from './new';
const axios = require('axios')  

function Map() {
	return(
		<div className = 'cont_item'>
			<h1>我是map组件</h1>
		</div>
		
	)
}


	class App extends React.Component{
		constructor(props){
			super(props)
			this.state = {
				msg:'lyx',
				navlist:['疫情地图','最新进展','广州疫情','新闻内容'],
				tabIndex:0,
				barStyle:{
					"left":"22px"
				},
				contStyle:{
					"transform" :"translate(0,0)"
				}

			}
		}
	// ------------------------------------------

		

		 render(){
		var navjsx=	this.state.navlist.map((item,index)=>{
					if(index === this.state.tabIndex){
						return(
							<div className = "navItem active" onClick = {(event)=>{this.tabClickEvent(index)}} key ={index}>
								{item}
							</div>
						)	
					}else{
						return(
							<div className = "navItem" onClick = {(event)=>{this.tabClickEvent(index)}}   key ={index}>
								{item}
							</div>
						)	
					}
			})
			 return (
			 <div className = "App">
			 		<div className= "nav ">
						 <div className= 'bar' style = {this.state.barStyle}></div>
						{navjsx}
					 </div>

					 <div className="cont" style ={this.state.contStyle}>
						<NewsCom></NewsCom>
						<Map></Map>
					 </div>
					
			 </div>
			  );
		 }
	// ----------	 ---------- 
	tabClickEvent = (index)=>{
				this.setState({
					barStyle:{
						"left":(index*88+22)+"px"
					},
					contStyle:{
						"transform" :`translate(${-index*375}px,0)`
					}

				})
		
	}
	
}

export default App;

````

解析:







## 18 插槽

组件中写入内容，这些内容可以被识别和控制。 Recat需要自己开发支持插槽的功能。

原理： 在父页面  引入的子组件组件中写入的HTML, 会挂载到放到子组件 props中。

````javascript
import React from 'react';
import ReactDOM from 'react-dom';




class Children extends React.Component {

  constructor(props) {
    super(props)
   this.state = {
   
   }}

        render(){
          console.log(this);
      //2. 在子元素的this。props中则挂载了插槽了的数据。 属性值和jsx，
      // 所以可以实现条件渲染在自己的dom中。
          return(
            <div className = 'Children-dom'>
                <h1>我是chidren</h1>
            {this.props.children}
            </div> 
          )
        }

}
// --------------------

class Clock extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
   fatherList : 'i is from father'
   }
  }
          render() {
           
              return(  
                <div>    
                  {this.props.children}
                      <h1>我是h1</h1>
                      <Children>  
             {/* 1. 插槽传值：在字标签中可以传入标签，dom 标签中的属性值，和state中的数据。 */}

                        <h1 data-id ='1'>我是parent的插槽 头部</h1>
                        <h1 data-id ='2'>我是parent的插槽 尾部</h1>
                          <span>  {this.state.fatherList}</span>
                      </Children>
                </div>
              )}

}


  ReactDOM.render(
    <Clock>
    </Clock> ,
    document.getElementById('root')
  );
````



## 19  路由



### 概念：

  根据不同的路径，显示不同的组件（内容）：React使用的库 react-router-dom;

安装:

````javascript
npm install react-router-dom --save       (--save保存版本信息) 
                                              "react-router-dom": "^5.2.0",
````

ReaterRouter ： 三大组件

Router: 所有路由租金的跟组件（底层组件），包裹路由规则的最外层容器。

Route:路由规则匹配组件，显示当前规则对应的组件。

Link: 路由跳转的组件。

注意： 如果要精确匹配，那么可以在route上设置 exacct  属性。（注意单词adj. 准确的，精密的；精确的）



### 路由的两种引入：

### hash 模式     

#/      #号就是hash的标志。 不发送请求

```jsx
import { HashRouter as Router, Route , Link} from 'react-router-dom'
```

### history 模式   

 /后边导向   需要后端配合

````javascript
  引入
import {BrowserRouter as Router, Route , Link} from 'react-router-dom'

````

### 总结：

 basename  设根路径

  route  映射路由和组件 关系

link  相当于a标签跳转

### 0. exact 精准匹配。

````javascript
第一种： 当有link标签时， 加载link中。
第二种： 没有link标签，只有route 标签时，加在route中。

 <Link to = '/product' exact>产品页</Link>
<Route path =  "/"    component = { ()=> (   <div> 首页1</div>) }></Route>



<Route path =  "/"  exact  component = { ()=> (   <div> 首页1</div>) }></Route>
                                               
````





#### 基本的路由模式 code

### 1. 常规的路由link跳转 和传值

APP.js  组件页面 挂载到index.js 主页面中

````javascript
import React from 'react';
import ReactDOM from 'react-dom';

import {BrowserRouter as Router, Link, Route} from 'react-router-dom'


function Me(props){
  console.log(props);
  return(
        <h1>Me</h1>
  )
}

function Home(props){
  console.log(props);
  return(
        <h1>Home</h1>
  )
}



function Produc(props){
  console.log(props);
  return(
        <h1>Produc</h1>
  )
}


  class App extends React.Component {
  constructor(props) {
    super(props)
   this.state = {
  
   }
  }
    render(){
      return(   

  <div id = 'app'>    
           <div> 所有页面都显示的普通页面</div>
   
   
         <Router >   
        
         <div className = 'nav'>
      
             <Link to = { { pathname:"/",search:"?sername=admin",hash:"#abc",state:{msg:"helloworld"}} }>Home</Link>
             <Link to = '/product'>产品页</Link>
             <Link to = '/me'>个人中心</Link>
         </div>
   
             <Route path = "/" exact component = {Home}></Route>
             <Route path =  "/product" component = {Produc}></Route>
             <Route path =  "/me" component = {Me}></Route>
   
         </Router>   
   </div>
 
      )
   
}
}
export default App;
````

#### Link to = { 变量}

````javascript
         <Router >   
         <div className = 'nav'>
             <Link to = { { pathname:"/",search:"?sername=admin",hash:"#abc",state:                                       {msg:"helloworld"}} }>Home</Link>
         
         </div>
             <Route path = "/" exact component = {Home}></Route>
         </Router> 

1. link to  后面的path和route标签，映射关系。
2. exact 精准匹配。  否则 /me 页面会显示  /的页面。
3. link传递的值。可以在组件中收到


        function Home(props){
          console.log(props);
          return(
                <h1>Home</h1>
          )
        }

点击会自动拼接
http://localhost:3000/?sername=admin#abc
````

###  2 path 传值

通过路由标签，link传值， route ： 键值， 组件中props对象中可以看到params下的值。

```javascript
        <Router >   
         <div className = 'nav'>
            <Link to = '/me/12345' replace >个人中心</Link>
         </div>
            <Route path =  "/me/:id"    component = {Me}></Route>
         </Router> 

浏览器地址
http://localhost:3000/me/12345
```









### 3.  Link 的 replace 路由切换跳转

替换栈 。  使用方法： 直接在Link 标签后内添加  replace 替换 属性。

````javascript
        <Router >   
         <div className = 'nav'>
             <Link to = '/me' replace >个人中心</Link>
         </div>
             <Route path =  "/me"    component = {Me}></Route>
         </Router> 
````





### 路由跳转，replace / push 区别

```
 push: a-b-c 可以回到上一级
 例： this.props.history.push('路由地址')
```

```
replace: a-b-c 回不到上一级 适用于登录后，不需要重新回到登页面
 例: this.props.history.replace('路由地址')
```

### 4 重定向组件

形式也是一个组件，所以也有props 对象。

概念： 如果访问到某个组件时，如果有重定向组件，那么就会修改页面路径，使得页面内容显示未错定向路径的内容。

引入  Redirect 方法

````javascript
import {BrowserRouter as Router, Link, Route, Redirect} from 'react-router-dom'
````



原理： 

假设 form表单登录的时候， 设置访问FormCom() 组件，这个组件就是登录页面，点击提交，

 组件内设置 ajax请求，获取用户权限，携带信息，跳转LoginInfo 组件， 组件内<Redirect to = "/login"></Redirect>    标签 ，跳转到 登录或者是 首页。



````javascript
import React from 'react';
// import ReactDOM from 'react-dom';

import {BrowserRouter as Router, Link, Route, Redirect} from 'react-router-dom'



function LoginInfo(props){    //重定向组件 

  if(props.location.state.login_state == 'success'){
    // 如果成功 定向到admin页面
    return <Redirect to = "/admin"> </Redirect> 
  }else{
    return <Redirect to = "/login"></Redirect> 
  }
}


function FormCom(){
   let dataobj = {
     pathname:"LoginInfo",
     state:{
       login_state:'success'
     }
   }

    return(
<div>
  <h1>表单验证模拟</h1>
    <Link to = {dataobj }>点击跳转至LoginInfo控制组件</Link>
    
</div>
    )
}

  class App extends React.Component {
    render(){
      return(   

            <div id = 'app'> 
          
         <Router >   
          <Route path =  "/"  exact  component = { ()=> (   <div> 首页1</div>) }></Route>
          <Route path =  "/form" exact  component = { FormCom }></Route>
          <Route path =  "/login" exact  component = { ()=> (   <div> login请重新登陆                           </div>) }>
          </Route>
          <Route path =  "/LoginInfo" exact  component = { LoginInfo }></Route>
          <Route path =  "/admin" exact   component = { ()=> (   <div> admin登录成功到                              admin</div>) }>
        </Route>
   
         </Router>   
   </div>
 
      )
}
}

export default App;




````



### 5 Switch   (n. 开关)  匹配 only one

应用场景：



```javascript
路由会一直匹配，直到查找完所有的路由映射。

1.假设没有exact 精准匹配， 进入home 首页也会显示。
 <Route path =  "/" 
 <Route path =  "/home" 
2.有exact 精准匹配，碰到两个path相同的，又会同时显示两个页面内容。
 <Route path =  "/"  exact  component = { ()=> (   <div> 首页1</div>) }></Route>  
  <Route path =  "/"  exact  component = { ()=> (   <div> 首页1</div>) }></Route>
 
                                                 
 Switch 作用： 匹配一条route，符合要求，就停止匹配。                                                                                          
```



使用方式:

````javascrpt

引入  Switch 方法  注意模块都是首字母大写

import {BrowserRouter as Router, Link, Route, Redirect, Switch} from 'react-router-dom'


包裹route 使用。
<Router >   
           <Switch>
          <Route path =  "/"  exact  component = { ()=> (   <div> 首页1</div>) }></Route>
           </Switch>
</Router> 


````

### 6 编程式路由  js控制

####   1.   push ( ) 跳转

子页面，点击跳转同时携带数据，  传值

```javascript




class Children extends React.Component {

  render(){
    return(   
          <div id = 'Children'>    
        <button onClick = { this.clickEvent}>  跳转到首页</button>
            我是 Children
        </div>
    )
  }
        clickEvent=()=>{  
            console.log(this.props.history.push("/",{name:"这是chilren传递的数据"}))
          }
          // push( ) 接受两个参数  第一个时路由path , 第二个是： 可以页面传值  目标组件的 props中的location-state 下挂载

  }
```

#### replace

#### go

```
clickEvent=()=>{  
          //  this.props.history.push("/",{name:"这是chilren传递的数据"})
          //  this.props.history.replace("/",{name:"这是chilren传递的数据"})
          this.props.history.go(-1)  //正数前进，负数后退。 历史堆栈中要有数据，否则不能跳转。

          }
```

### 7  动态路由

解析： 

正常老说：   path =  "/"    只能在  localhost:3000/   时可以访问。 不能加参数

path =  "/:id"  这种， 后边可以加参数，变化的参数也可以。 动态。 

同样 props中可以查看数据

````javascript


<Route path =  "/:id"  exact  component = { shouye }></Route>

````



## 20 Redux  数据仓库

解决React 数据管理（状态管理） ，用于中大型，数据比较庞大，组件之间数据交互多的情况下使用。

作者：如果你不知道是否需要使用Redux,那么你就不需要它！

解决组件的数据通信。

解决书和交互 较多的应用。

关键点：

  Store:  数据仓库，保存数据的地方。

State :state 是一个对象，数据仓库里的所有数据都放到1个state里。

Action : 1 个动作， 触发数据改变的方法。

Dispatch : 将动作触发成方法

Reducer ：是一个函数，通过获取动作，改变数据，生成一个新state. 从而改变页面。



案例： 点击加减事件，控制仓库的数据变化

###  第一种 1. 安装 ：  redux

```javascript
npm install redux --save
```

### 2. 引入

```javascript
// 引入仓库和 解构创建仓库的方法

import Redux , {creatStore, createStore}  from 'redux' 
这个例子只用了这一个 createStore

```

### 3.   根据业务逻辑创建函数 

```javascript
// 2. 创建函数  通过动作 用于创建新的state   参数：传入需要修改的数据 和方法 (形参)
const reducer = function(state = { num: 0 }, action ){

    switch(action.type){
      case "add_" :
        state.num++;
        break;
        case "decrement_" :
          state.num--;
          break;
          default:
          break;
    }
    return {...state} // 解构，每次生成新的数据 返回
}
```

### 4. 创建仓库  把业务函数放入仓库

```javascript
const store = createStore(reducer) //1. 创建仓库  放置要给函数，专门用于管理状态
```

###  5 两个点击事件

```javascript
function add(){

  //通过仓库的方法 dispatch 进行修改数据
  store.dispatch({type:"add_" ,name:'lyx'}) //传递数据到第二步 创建的函数中 ->action中
  console.log(store.getState());

}

function decrement(){
  //通过仓库的方法 dispatch 进行修改数据
  store.dispatch({type:"decrement_"})
  console.log(store.getState());
}
```

### 6 使用仓库数据的面板   组件

```javascript
  const Counter  = function(props){
      return (
        <div>
        <h1>计数数量：{ store.getState().num }</h1>
        <button onClick = {add}>计数++</button>
        <button onClick = {decrement }>计数--</button>
        </div>
      )
  }
```

7.  数据修改后，监听 和渲染页面

````javascript
store.subscribe(()=>{//监听数据变化 重新渲染  react时单向数据流

  ReactDOM.render( <App></App> ,document.getElementById('root'));
})
````



### 完整代码

### App.js

````javascript
import React from 'react';
// import ReactDOM from 'react-dom';

// 引入仓库和 解构创建仓库的方法
import Redux , {creatStore, createStore}  from 'redux' 

// 2. 创建函数  通过动作 用于创建新的state   参数：传入需要修改的数据 和方法 (形参)
const reducer = function(state = { num: 0 }, action ){
console.log(action);
    switch(action.type){
      case "add_" :
        state.num++;
        break;
        case "decrement_" :
          state.num--;
          break;
          default:
          break;
    }
    return {...state} // 解构，每次生成新的数据 返回
}

const store = createStore(reducer) //1. 创建仓库  放置要给函数，专门用于管理状态

function add(){

  //通过仓库的方法 dispatch 进行修改数据
  store.dispatch({type:"add_" ,name:'lyx'}) //传递数据到第二步 创建的函数中 ->action中
  console.log(store.getState());

}

function decrement(){
  //通过仓库的方法 dispatch 进行修改数据
  store.dispatch({type:"decrement_"})
  console.log(store.getState());
}

// 函数式的计数器

  const Counter  = function(props){
      return (
        <div>
        <h1>计数数量：{ store.getState().num }</h1>
        <button onClick = {add}>计数++</button>
        <button onClick = {decrement }>计数--</button>
        </div>
      )
  }



  class App extends React.Component {
    render(){
      return(   
            <div id = 'app'>    
                    我是 app组件
                    <Counter></Counter>
          </div>
      )
}}



export {
   App ,store
}

````

### index.js

````javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Redux , {creatStore, createStore}  from 'redux' 

import {App ,store } from './App';

  ReactDOM.render( <App></App> ,document.getElementById('root'));


store.subscribe(()=>{//监听数据变化 重新渲染  react时单向数据流

  ReactDOM.render( <App></App> ,document.getElementById('root'));
})
````



##  第二种 react-redux

概念： 

Provider组件： 自动将store里的state和组件进行关联。

MapStatetoProps： 这个函数用于将store的state映射到组件的 props

mapdispatchToProps： 将store中的dispatch 映射到组件的props里，实现了方法的共享。

Connect 方法： 将组件和数据（方法）进行连接。

案例： 和上一个 一样

### 1 引入包

````javascript
npm install react-redux --save
````

### 2 引入方法

```javascript
import  {createStore}  from 'redux' 

import  {Provider, connect }  from 'react-redux' 
```

关键点把握

createStore

```javascript
  function reducer(state={num:0},action){

    switch(action.type){
      case "add":
        state.num++;
        break;

        default:
          break

    }
  return {...state}
  }

   const store = createStore(reducer)
```



Provider（   n. 供应者；养家者）  自动将store里的state和组件进行关联。

````javascript
   ReactDOM.render(
    <Provider store= {store}>
    <App></App>
    </Provider>,
    document.getElementById('root')
    )
````



connect    将组件和数据（方法）进行连接。

```javascript
 const App = connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)
```







### 3   数据的获取，数据的修改

要state映射到组件的props中，将修改数据的方法映射到组件的props中。

两个映射函数

```javascript
//将state映射到props函数
function mapStateToProps(state){
    return{
      value:state.num
    }
}

//将修改state数据的方法，映射到props  默认会传入store里的dispath方法
function mapDispatchToProps(dispatch){
  return{
   onAddClick:()=>{dispatch(addAction)}
  }
}
```

### 4  形成新的组件

```javascript
// 将上面2个方法，将数据仓库的state和修改states的方法映射到组件上，形成新的组件。

const App = connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)
```

### 5  原组件获得方法和属性值

```javascript
class Counter extends React.Component{

    render(){
      //计数，通过stroe的state传给props,直接通过props就可以将state的数据获取
      const value = this.props.value
      const onAddClick = this.props.onAddClick;
      // 等同于vuex的 mapMutation mapState

      return(
       <div>
         <h1>技术的数量：{value}</h1>
         <button onClick = {onAddClick}> 数字+1</button>
       </div>
      )
    }
}
```



### 完整代码  index.js

````javascript
import React from 'react';
import ReactDOM from 'react-dom';


import  {createStore}  from 'redux' 
import  {Provider, connect }  from 'react-redux' 
// Provider  渲染标签

class Counter extends React.Component{

    render(){
      console.log(this);
      //计数，通过stroe的state传给props,直接通过props就可以将state的数据获取
      const value = this.props.value
      const onAddClick = this.props.onAddClick;
      // 等同于vuex的 mapMutation mapState

      return(
       <div>
         <h1>技术的数量：{value}</h1>
         <button onClick = {onAddClick}> 数字+1</button>
       </div>
      )
    }
}

  const addAction = {
    type:"add"
  }


  function reducer(state={num:0},action){

    switch(action.type){
      case "add":
        state.num++;
        break;

        default:
          break

    }
  return {...state}
  }

   const store = createStore(reducer)


//将state映射到props函数
function mapStateToProps(state){
    return{
      value:state.num
    }
}

//将修改state数据的方法，映射到props  默认会传入store里的dispath方法
function mapDispatchToProps(dispatch){
  return{
   onAddClick:()=>{dispatch(addAction)}
  }
}

// 将上面2个方法，将数据仓库的state和修改states的方法映射到组件上，形成新的组件。

const App = connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)


  // ReactDOM.render( <App></App> ,document.getElementById('root'));


    ReactDOM.render(
    <Provider store= {store}>
    <App></App>
    </Provider>,
    document.getElementById('root')
    )


````



稍作注释：

````javascript
import React from 'react';
import ReactDOM from 'react-dom';


import  {createStore}  from 'redux' 
import  {Provider, connect }  from 'react-redux' 
// Provider  渲染标签

// 第一步： 构建类组件   目的： 可以使用类组件的props
class Counter extends React.Component{

    render(){
      console.log(this);
      //计数，通过stroe的state传给props,直接通过props就可以将state的数据获取
      const value = this.props.value
      const onAddClick = this.props.onAddClick;
      // 等同于vuex的 mapMutation mapState

      return(
       <div>
         <h1>技术的数量：{value}</h1>
         <button onClick = {onAddClick}> 数字+1</button>
       </div>
      )
    }
}

// 第二步： 构建业务逻辑  初始化仓库
  function reducer(state={num:0},action){

    switch(action.type){
      case "add":
        state.num++;
        break;

        default:
          break

    }
  return {...state}
  }

   const store = createStore(reducer)


//将state映射到props函数
function mapStateToProps(state){
    return{
      value:state.num
    }
}

const addAction = {
  type:"add"
}

//将修改state数据的方法，映射到props  默认会传入store里的dispath方法
function mapDispatchToProps(dispatch){
  return{
   onAddClick:()=>{dispatch(addAction)}
  }
}

// 将上面2个方法，将数据仓库的state和修改states的方法映射到组件上，形成新的组件。

const App = connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)


  // ReactDOM.render( <App></App> ,document.getElementById('root'));

  // Provider 自动将store里的state和组件进行关联。
    ReactDOM.render(
    <Provider store= {store}>
    <App></App>
    </Provider>,
    document.getElementById('root')
    )


````
