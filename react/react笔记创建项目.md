## 碰到的问题：

```
当前版本
"react": "^18.2.0",
"react-dom": "^18.2.0",

npm -v  //8.5.0
```

### 1  api报错

index.js

```
import  ReactDOM  from "React"
ReactDOM.render(<div>55</div>, document.getElementById('root'))
报错如下：
_default(...).render is not a function
```

原因：  [React](https://so.csdn.net/so/search?q=React&spm=1001.2101.3001.7020)团队目前推出最新的版本为18.0，在18.0版本中，React不再支持 ReactDOM.render，

### 2 className

 class 声明关键字 避错



# 创建项目

#### 先查看自己有没有安装node.js 和 npm

## 1.创建React项目

我们可以通过安装create-react-app来创建React项目。

安装命令：

```
npm install -g create-react-app
create-react-app demo  
```

(demo是你项目的名称)

进入刚刚创建的demo目录中：

```
cd demo 
```

（一定要进入demo项目 目录中才可以启动项目哟！！！）

启动项目：

```
npm start
```

稍等片刻，则会自动打开一个网页！！！

（可能会遇到卡在    Starting the development server... 这里

原因  ：因为电脑上的防火墙阻止了启动浏览器

解决办法：更改防火墙设置  并且重启电脑

## 安装`react`的路由

```
cnpm install --save react-router-dom
```













