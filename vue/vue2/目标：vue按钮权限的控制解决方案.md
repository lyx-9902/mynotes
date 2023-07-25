### 目标：vue按钮权限的控制解决方案

### 准备知识点：

## (一)Vue.directive指令(自定义指令)

 webpack中案例

#### main.js中写入如下代码：

#### 1. 怎么配置   

#### 自定义指令的生命周期

```
Vue.directive('hello', {
  // 当被绑定的元素插入到 DOM 中时……被调用
  inserted: function(el,binding,vnode) {
    el.style["color"]= binding.value;
  },
  update: function() {//所在组件的 VNode 更新时调用
		
			},
			componentUpdated: function() {//子组件和父组件都更新时调用
			
			},
			unbind: function() {//只调用一次，指令与元素解绑时调用
		
			},
})
---------------写在vue实例之前。
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```

#### 2. 怎么调用：

不管在哪个组件中，

只要标签中包含 v-hello 这个自定义属性。就等于执行自定义函数。

```
<span v-hello="color">{{message}}</span> 

  data() {
    return {
      message: 10,
      color: "green",
    };
  },
```

#### 3 默认写法

一般使用插入功能，可以简写如下

```
第一种写法：
Vue.directive("hello",function(el,binding,vnode){
  console.log(el,binding,vnode )
  el.style["color"]= binding.value;
 })

第二种写法：
Vue.directive('hello', {
  // 当被绑定的元素插入到 DOM 中时……被调用
  inserted: function(el,binding,vnode) {
    console.log(el)
    el.style["color"]= binding.value;
  }
})
总结：1.当directive中传入一个回调函数时，默认是inserted dom插入时执行一次。
     注意：2. 上述代码写到实例之前。
```

#### 4.可以使用参数说明

这里要说明的就是指令写的是v-hello,但是我们用directive的时候前面不用加v-了，直接输入指令即可
 可以看到数字也变成绿色了，说明自定义指令也起作用了。

el : 指令所绑定的元素，可以用来直接操作DOM

binding: 一个对象，包含指令的很多信息

vnode: VUE编译生成的虚拟节点

```
<span v-hello="color">{{message}}</span>  
v-hello="color" 可以传字符串  对象 和数组 
v-hello="[color ,20]" 

```

参考：

[Vue.directive指令(自定义指令)](https://www.jianshu.com/p/13398358b5b4)



## (二) sessionStorage

官方：

`sessionStorage` 属性允许你访问一个，对应当前源的 session [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage) 对象。它与 [`localStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/localStorage) 相似，不同之处在于 `localStorage` 里面存储的数据没有过期时间设置，而存储在 `sessionStorage` 里面的数据在页面会话结束时会被清除。

查看方式： chrome  浏览器的 Application   下的 Storage    ->   sessionStorage 

简单来说： 设置没有过期时间， 刷新页面不掉数据。  除非关掉页面或者手动去localStorage清除，和使用官方方法清除。

## 语法

```
// 保存数据到 sessionStorage
sessionStorage.setItem('key', 'value');

// 从 sessionStorage 获取数据
let data = sessionStorage.getItem('key');

// 从 sessionStorage 删除保存的数据
sessionStorage.removeItem('key');

// 从 sessionStorage 删除所有保存的数据
sessionStorage.clear();
```



参考：

[Window.sessionStorage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage#%E6%B5%8F%E8%A7%88%E5%99%A8%E5%85%BC%E5%AE%B9%E6%80%A7)



### （三 ）  项目使用：

均在main.js中。

```
前提： 路由中的name 先设置好。用于区分进入的页面是那个一个。

第一步：设置路由守卫   进入页面调用方法
router.afterEach(route => {
  // 除了访问跳转中间件 toJump， 访问页面时会去获取该页面的按钮权限
  if (route.name != "toJump") {
    getButtonPermission(route.name);
  }
})

调用的方法：作用从后台获取权限数据，存入到本地sessionStorage。         
/**
 * @description 获取按钮权限
 * @param {String} code 页面编码
 * */
function getButtonPermission(pageCode) {
  Vue.prototype.$axios.defaults.withCredentials = true;
  Vue.prototype.$axios
    .post(Vue.prototype.$auth + "/menu/getMenuByProCode", { proCode: "jtyj" })
    .then((res) => {
      let code = res.data.code;
      if (code === 200) {
        let data = res.data.resultData;
        console.log(data)
        data.forEach(item => {
          if (item.id == pageCode) {
            sessionStorage.setItem("buttonPermission", JSON.stringify(item.buttonList));
          }
        })
      }
    })
    .catch((error) => {
      console.log(error);
    });
}

第二步
 设置自定义指令   作用是：当标签中包含指定 btn-has时， 获取传入的参数，进行判断，是否显示或移除当前dom.
/**
 * 按钮权限判断指令
 */
Vue.directive('btn-has', {
  // 当被绑定的元素插入到 DOM 中时
  inserted: function (el, binding) {
    let params = binding.value;
    if (params) {
      let flag = Vue.prototype.btnPermission(params.split(',')[0], params.split(',')[1]);
      if (!flag) {
        el.remove();
      }
    }
  }
});

第三步：
组件中使用自定义指令  注意前缀：v- 

 v-btn-has="'common,add'"
 <el-button
          type="primary"
          @click="dialogVisible = true;dialogTitle = '新增';dialogForm.orgTypeId='0'"
          v-btn-has="'common,add'"
        >新增</el-button>

```

参考：

[vue学习011:按钮级权限控制](https://www.jianshu.com/p/e50633a9005e)















