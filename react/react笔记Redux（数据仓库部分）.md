##  Redux  数据仓库

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

### 第一种 1. 安装 ：  redux

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

### 5 两个点击事件

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

7. 数据修改后，监听 和渲染页面

```javascript
store.subscribe(()=>{//监听数据变化 重新渲染  react时单向数据流

  ReactDOM.render( <App></App> ,document.getElementById('root'));
})
```



### 完整代码

### App.js

```javascript
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

```

### index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Redux , {creatStore, createStore}  from 'redux' 

import {App ,store } from './App';

  ReactDOM.render( <App></App> ,document.getElementById('root'));


store.subscribe(()=>{//监听数据变化 重新渲染  react时单向数据流

  ReactDOM.render( <App></App> ,document.getElementById('root'));
})
```



## 第二种 react-redux

概念： 

Provider组件： 自动将store里的state和组件进行关联。

MapStatetoProps： 这个函数用于将store的state映射到组件的 props

mapdispatchToProps： 将store中的dispatch 映射到组件的props里，实现了方法的共享。

Connect 方法： 将组件和数据（方法）进行连接。

案例： 和上一个 一样

### 1 引入包

```javascript
npm install react-redux --save
```

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

```javascript
   ReactDOM.render(
    <Provider store= {store}>
    <App></App>
    </Provider>,
    document.getElementById('root')
    )
```



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

```javascript
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


```



稍作注释：

```javascript
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


```

本节结束