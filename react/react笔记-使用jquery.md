## react中使用jquery 语法



```javascript npm install jquery
 npm install jquery
```



引入

import $ from  'jquery'

```javascript
import React from 'react';
import './css/App.css'
import { Button } from 'antd';
import $ from  'jquery'

let slider_img =[
  'https://cdn.jsdelivr.net/gh/xaoxuu/cdn-wallpaper/abstract/41F215B9-261F-48B4-80B5-4E86E165259E.jpeg'
,"https://cdn.jsdelivr.net/gh/xaoxuu/cdn-wallpaper/abstract/B18FCBB3-67FD-48CC-B4F3-457BA145F17A.jpeg"
]


class App extends React.Component{

  constructor(props) {
    super(props)
      this.state = {
      }
  }

  componentWillMount(){
    console.log(' CompontWillMount： 组件将要渲染')
   
  }

componentDidMount(){
  window.addEventListener('resize', this.handleResize.bind(this)) 
}

componentWillUnmount() {  // 防止 this混乱   去掉this
  window.removeEventListener('resize', this.handleResize.bind(this))
}

        handleResize(e){
          $('.App-slideshow').css({
            // marginLeft: document.body.clientWidth*0.3+"px"
          })

         console.log($('.App-slideshow'));
        console.log( document.body.offsetWidth );
        console.log(  document.body.clientWidth);
        }

  render(){
  return (
      <header className="App-slideshow">
          <div className = "slideshow_item">
               <img src= {slider_img[0] } alt="this is img" />
          </div>
      </header>
 
  );

}
}

export default App;

```



## 