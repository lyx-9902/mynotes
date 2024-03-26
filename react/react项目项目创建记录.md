# react项目项目创建记录

## css插件

```
npm i --save sass   

文件命名
Child.module.scss   
```

## 安装请求插件 axios

```
npm i axios
```

## 配置跨域

```
npm i --save http-proxy-middleware

npm install http-proxy-middleware --save
```

## 安装路由

```
npm i --save-dev react-router-dom

npm i --save-dev react-router-dom
npm uninstall react-router-dom
```



react18  对应router6

react17  对应 router 5

## 安装antd 

这里使用的是

   "antd": "^4.14.0",

样式要引入一下

修改 `src/App.css`，在文件顶部引入 `antd/dist/antd.css`。

### npm 模块 移除

只有加上对应参数才可以：-S, –save：dependencies

-D, –save-dev：devDependencies

-O, –save-optional：optionalDependencies

比如：

npm uninstall element-ui -S

就可以在卸载element-ui的同时，把其从dependencies中删除掉了。

npm install/uninstall xxx是，只是安装／卸载对应模块

只有加上：

–save

–save-dev

等参数，才能把对应模块版本要求，加入到／删除掉 package.json中。





## antd ui使用常识

menu组件

| defaultSelectedKeys                | 初始选中的菜单项 key 数组 |
| ---------------------------------- | ------------------------- |
| 默认选中    会把menu变成非受控组件 |                           |



| selectedKeys                    | 当前选中的菜单项 key 数组 |
| ------------------------------- | ------------------------- |
| 受控组件  刷新页面 data同时更新 |                           |



