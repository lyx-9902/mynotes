# vue vuex+keep-alive进阶用法(灵活缓存页面，主要是移动端)



https://blog.csdn.net/u014678583/article/details/111384354

### **注意：每个页面都要添加name，name:"页面名称'，不然不起作用**

### 1、在App.vue中，编写如下代码

```
<template>
    <div id="app">
        <!-- include 需要缓存的组件 -->
        <keep-alive :include="includeList">
            <router-view />
        </keep-alive>
    </div>
</template>
 
<script>
import { mapState } from 'vuex';
export default {
    data(){
        return{
        }    
    },
    computed: {
        ...mapState(['includeList'])
    },
}
```

### 2、在store.js中

```
import Vue from 'vue'
import Vuex from 'vuex'
 
Vue.use(Vuex)
 
export default new Vuex.Store({
  state: {
    includeList: ['Home', 'Center', 'Cart'], //初始化缓存页面，一般来说就用tabbar底部的导航，自定义添加
  },
  mutations: {
    //插入缓存数组
    setInclude(state, data) {
      var index = state.includeList.indexOf(data);
      if (index == -1) {
        state.includeList.push(data)
      }
    },
    //删除对应缓存字段
    del_include(state, data) {
      var index = state.includeList.indexOf(data);
      if (index > -1) {
        state.includeList.splice(index, 1)
      }
    },
  },
 
  actions: {
  },
  modules: {
  }
})
```

### 3、tabbar页面使用，主要是底部导航那几个一级页面

```
export default {
    name:'Home',
 
    beforeRouteEnter(to, from, next) {
        next(vm => {
            document.querySelector('body').setAttribute('style', 'background-                   color:#f6f6f6');
        })
    },
    beforeRouteLeave(to, from, next) {
        if (from.name === 'Home') {
            this.$store.commit('setInclude', 'Home')
        } 
        document.querySelector('body').removeAttribute('style')
        next()
    },
    created(){
        //初始化一些数据
    },
    //keep-alive缓存，替代created()执行，首次不执行，之后只要缓存生效了每次都会执行。刷新时created与     activated都会执行
    activated(){
        //要执行的操作
    },
    //卸载
    deactivated() {
        
    },
}
```

# vue vuex+keep-alive进阶用法(灵活缓存页面，主要是移动端)

https://blog.csdn.net/u014678583/article/details/111384354?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-2&spm=1001.2101.3001.4242.1











