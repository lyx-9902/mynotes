# vue3笔记2024

## 简介

Pinia 替代vuex状态管理插件。



2020.9.8，vue3发布3.0    截止到2023.10月 最新本本3.3.4

版本特点：

 1.打包大小减少 41%，初次渲染快 55%，更新渲染快 133% ，内存减少 54% 。

2. 源码的升级   使用 Proxy 代替 defineProperty 实现响应式。重写虚拟 DOM 的实现和 Tree-shaking.
3. 拥抱TS



### 新的特性

Composition API (组合API)

 setup

ref  reactive  构建响应式数据

computed 与watch   计算属性和数据监听

新的内置组件

Fragment  

Teleport    <teleport to="body">插入节点

Suspense       自组件中，有异步事件，包裹组件。

其他改变

新的生命周期钩子

data 选项应始终被生命为一个函数

## vue3的相关原理

#### 数据响应原理

Proxy 代理 这个是原生js自带的方法  window自带

vue3.0 开始 Proxy代替Object.defineProperty，产生了一些列疑惑。

- Proxy是什么？
- Proxy能干什么？
- Vue用Object.defineProperty干了什么？
- 为什么用Proxy代替Object.defineProperty？

补充知识点：

Proxy： Vue3中的响应式数据是通过ES6的Proxy来实现的。那么什么是Proxy。

MDN定义：Proxy 对象用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。

通俗的讲Proxy是一个对象操作的拦截器，拦截对目标对象的操作，进行一些自定义的行为，一种分层的思想有点类似。

案例：

```
let target = {};
let p = new Proxy(target, {});

p.a = 37;   // 操作转发到目标

console.log(target.a);    // 37. 操作已经被正确地转发
（可以看到，通过操作p，修改了target对象的数据。）

```

[参考](https://blog.csdn.net/sj15942331889/article/details/100210046?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163186967516780262520842%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163186967516780262520842&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-100210046.first_rank_v2_pc_rank_v29&utm_term=Proxy&spm=1018.2226.3001.4187)





### 其他自己总结tips

```
1  vue3中， 组件中原来只能有一个根dom节点. 现在不做限制，可以多个。建议还是保持一个。



```





## 2 项目创建

### 创建方式

vue-cli创建    脚手架   （基于webpack）

```
vue create 项目名称
```



vite（推荐） 官方开发的提高编译的工具，替换vue-cli

```
npm create vue@latest  安装最新版

npm i  初始化依赖
npm run dev 启动项目
```



拓展：

vite 是新一代前端构建工具，官网地址:https://vitejs.cn
vite 的优势如
轻量快速的热重载(HMR)，能实现极速的服务启动。
对 Typescript、JSX、
等支持开箱即用。CSS
真正的按需编译，不再等待整个应用编译完成。

总结：webpack是入口，加载路由，加载所有页面。  vite进入路由，等待要查看那个路由，然后再加载处理。  效果：服务启动快，开发过程，友好。

### 安装两个插件 

以下案例使用vite 打包器 ， 代码编辑器 vscode

安装两个插件    vue3+TS 项目 

```
Vue Language Features (Volar)

TypeScript Vue Plugin (Volar)

设置-》 搜索 Volar -->   找到这个  Vue >Auto Insert: Dot Value
 作用： 自动加   .value 辅助
```



一个组件最简单的配置

```vue
<template>

</template>

<script setup lang="ts">    标签中加setup 语法糖写法

</script>

<style scoped>

</style>
```

## 3.Vue3核心语法

### 3.1【Options API和Composition】

vue2     Options API (基于选项的 API )

vue3   [Composition API](https://blog.csdn.net/weixin_53919192/article/details/126555958#d84051de)  （组合api）

首先，vue3是vue2的升级版本，所以，vue2的data,methods，computed 等都可以在vue3中使用。

vue相当于，通过新增一个配置项，setup(), 使得可以将 data,metnods，computed 等都可以放到里面，让你一个页面中的分散的代码，可以以功能或自定义，放到一起。当然要使用新的写法，放在setup中，才能发挥作用。

### 3.2 【拉开序幕的setup】

#### vue3中，setup和  data,methods的关系？同时出现，谁优先？

1. setup实质作为一个配置项，可以 和data，methods可以同时存在。（但是严禁混写）
2. data可以读取 setup中的东西，但是sutup不能读取旧配置中的东西。

setup语法糖

#### 一般写法

```vue

<template>
  <div>
    <p>数据{{ age }}</p>
  </div>
</template>
<script lang="ts">
export default {
  name: 'Person',
  beforeCreate() {
    console.log("beforeCreate");
  },
  setup() {
    console.log("setup")   // 执行时机  在beforeCreate之前   setup中，没有this; 

    let name = "tom"; // name不是响应式
    let age = 10;

    // 方法
    function change() {
      console.log(age);

      age++
    }

    // return function(){
    //   return "99999"
    // }
    // 或者是
    // return ()=>"哈哈"    // 可以返回一个函数，这时页面直接显示你return的东西。无视模板内容

    return { name, change, age }  //变量和方法 需要抛出去才能在template模板中使用
  }
}

</script>
<style scoped></style>

```

语法糖写法

变化，就是你不需要return出去了，默认处理。 引入组件也不需要注册使用，可以直接使用。

```vue

<template>
  <div>
    <p>数据{{ age }}</p>
  </div>
</template>

<script lang="ts" setup>

const age = 10

</script>

<style scoped></style>

```

### vue3中的组件name命名问题

一般情况下，组件名称就是name, vue3中，可以新增一个script标签，写name

```vue

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
  </div>
</template>
<script lang="ts">
export default {
  name:"person" // 修改新名字
}
</script>

<script setup lang="ts">
</script>
```

也可以使用插件

```
cnpm i vite-plugin-vue-setup-extend -D
```

vite.config.ts 里

```json
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueSetupExtend from "vite-plugin-vue-setup-extend"  < --- 这里

export default defineConfig({
  plugins: [
    vue(),
    vueSetupExtend() < --- 这里
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})

```

组件中

```vue
<script setup lang="ts" name="Person234">
</script>
```

### 3.3 [ref reactive 数据响应式 ]

1. reactive必须传递一个对象

2. ref的本质其实还是reactive，系统会自动更具我们给ref传入的值将他装换成reactive（{value：xx}）

3. ref 注意点：在Vue中使用ref的值不用通过Value来获取，在JS中使用ref的值必须通过Value来获取。

   为什么是这样，参看vue3的响应原理。

**ref**

```
处理简单数据  const message = ref("11")
其实ref也可以定义obj，但是使用的时候，同样需要 xx.value，才能碰到数据。
```

**reactive**

```
处理复杂数据  const list = reactive({ data:[12]})

```

数据可以区分为：  响应式数据， 普通对象  

```vue

<template>
  <div class="greetings">
    <button @click="test">修改</button>
    {{ list }}
  <br>
  {{ message }}   //直接使用
  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive } from "vue"

const message = ref("11")

const list = reactive({
  data:[12]
})

const test = () => {

  message.value = 99;  //使用简单变量  修改时需要  xx.value操作

  list.data = [111,22,33]  //使用复杂变量

}

</script>


<style scoped></style>
```

总结

宏观角度看

1. ref 用来定义:基本类型数据、对象类型数据
2. 2.reactive 用来定义:对象类型数据。

区别:

1. ref 创建的变量必须使用.value(可以使用 volar 插件自动添加 .value)。

2. reactive 重新分配一个新对象，会失去响应式(可以使用 0bject.assign 去整体替换) ;不能整体修改；

    

   ```vue
   Object.assign(car,{brand:'奥拓'price:1})
   ```

   

使用原则:

1.若需要一个基本类型的响应式数据，必须使用ref
2.若需要一个响应式对象，层级不深，ref、reactive 都可以。
3.若需要一个响应式对象，目层级较深，推荐使用 reactive 。

##### .value的知识点

```tsx
// 第一种： ref类型
let num = ref(10);
{ { num } }   // 模板中直接h使用
console.log(num.value);  // js中，需要.value

// 第二种

let obj = reactive({
  a: 1,
  b: ref(3)
})
// obj.b   // js中，直接使用   原因： b在reactive中， 使用时自动解包
```







### 3.4 [ toRef  toRefs ]

响应式解构

toRef    解构一个   toRef(person,"age")

toRefs    解构多个   let { name, age } = toRefs(person);

```vue

<template>
  <div class="greetings">
    {{ name + age }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef } from "vue"

const person = reactive({
  name: "张三",
  age: 20
})
// let { name, age } = person; //  不加的话，只是对新的变量的操作，页面不会有变化
let { name, age } = toRefs(person); //toRefs处理响应数据，结构后，仍然是响应式的，
let nl = toRef(person,"age") // 单独结构指定属性

const change = () => {
  // age.value +=1
  nl.value +=1

  console.log(age.value,person.age);  // 只要修改的是同一个源数据，其他的也会一起变化
}

</script>
```

使用场景： 在后台返回的数据中，十几个属性，结构出来需要修改的一个，操作变量。



### 3.5 [computed 计算属性]

计算属性特性： 

有缓存   计算一次，可以多次使用。  methods 没有缓存，调用一次，就重新执行一次。

触发计算属性重新计算的条件，是依赖的数据有变化。

  计算属性的只读

```vue
<template>
  <div class="greetings">
    {{ fullName}}
    <br>
    <input v-model="firstName">
  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed } from "vue"

let firstName = ref("zhang")
let lastName = ref("san")

使用方法，从vue引出computed方法

let fullName = computed(() => {
  console.log(1)
  return firstName.value.slice(0, 1).toUpperCase() + 
      firstName.value.slice(1) + "-" + lastName.value
})
</script>
```

计算属性的只读 + 修改 

  修改的前提是，你知道变化的规律。这样 computed（{get, set}）入参，自定义逻辑。达到修改计算属性的目的

```vue
  <div class="greetings">
    {{ fullName }}
    <br>
    <input v-model="firstName">
    <button @click="changeFullName">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed } from "vue"

let firstName = ref("zhang")
let lastName = ref("san")

// fullName的   计算属性的只读写法
// let fullName = computed(() => {
//   return firstName.value.slice(0, 1).toUpperCase() + firstName.value.slice(1) + "-" + lastName.value
// })


// fullName的   计算属性的只读 + 修改 写法
let fullName = computed({
  get() {
    return firstName.value.slice(0, 1).toUpperCase() + firstName.value.slice(1) + "-" + lastName.value
  }, set(val) {
    console.log(val);
    // val 如果有人直接修改fullName 就是这个值
    const [str1,str2 ] = val.split("-")
    firstName.value = str1;
    lastName.value = str2

  }
})

function changeFullName() {
  fullName.value = "li-si"
}

</script>
```

###  3.6 [watch]

作用 : 监视数据的变化 (和 Vue2 中的 watch 作用一致)

特点: Vue3 中的 watch 只能监视以下四种数据

```
1.ref 定义的数据。
2.reactive 定义的数据,
3.函数返回一个值(getter 函数)。
4.一个包含上述内容的数组。
```

getter 函数指：有返回值的函数

```
（）=>{ returen 10}
```



#### 情况一 ref基本数据类型

监视ref定义的基本数据类型

```vue

<template>
  <div class="greetings">
    {{ num }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed, watch } from "vue"

let num = ref(10)

function change() {
  num.value++
}

//  监听数据变化   和停止监听
const stopWatch =  watch(num, (newVal, oldVal) => {
  console.log("变化了", newVal);
  if(newVal >= 15){
    stopWatch() //   num大于15后，停止监视
  }
})

</script>
```

#### 情况二 ref 对象类型

监视 ref 定义的【对象类型】数据:直接写数据名，

监视的是对象的【地址值】，若想监视对象内部的数据，要手动开启深度监视。

```vue

<template>
  <div class="greetings">
    {{ person }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed, watch } from "vue"

let person = ref({
  name: "tom",
  age: 20
})

function change() {
  person.value.age++   //没有反应
    // person.value = {name:"tom",age:21} //有反应
}
// watch 第一个参数：监听的数据 第二个参数：监听的回调 第三个：配置对象 （deep, immediate ）
// 1. 直接监听ref创建的对象    修改age 是没有反应的
// 2. 要监听指定属性  加深度监听配置参数
// 3. 注意点：newVal, oldVal 两个值，可以一样，可能不一样
watch(person, (newVal, oldVal) => {
  console.log("变化了", newVal);

},{deep:true,immediate:true})

// deep 深度监听  immediate立即监听 页面一加载，就打印一次

</script>
```

#### 情况三 reactive

reactive 定义的对象类型 数据， 默认开启深度监视 并且不能关闭

```vue

<template>
  <div class="greetings">
    {{ person }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed, watch } from "vue"

let person = reactive({
  name: "tom",
  age: 20
})


  function change() {
  //  person.age++
  Object.assign(person,{name:"li",age:80}) 
      // 实质整体的对象地址执行 ，根本就没有变化。只是内部的值发生了变化;也正是这样，newVal, oldVal始终是一样的。
  }
// reactive 定义的对象类型 数据， 默认开启深度监视 并且不能关闭
watch(person, (newVal, oldVal) => {
  console.log("变化了", newVal);
})

</script>
```



#### 情况四 数据中的某个属性

监视 ref 或 reactive 定义的【对象类型】数据中的某个属性，

注意点如下
1.若该属性值不是【对象类型】，需要写成函数形式
2.若该属性值是 依然是【对象类型】，可直接编，也可写成函数，不过建议写成函数

不管是什么类型：直接函数式， 没变化加deep:true 配置。

```vue

<template>
  <div class="greetings">
    {{ person }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed, watch } from "vue"

let person = reactive({
  name: "tom",
  age: 20,
  car: {
    c1: "大众",
    c2: "奥迪"
  }
})

function change() {
  person.car.c1 +='-'
}
//情况四： 监听响应式对象中的某一个属性， 该属性是基本类型的，要写成函数式
// watch(()=>person.age, (newVal, oldVal) => {
//   console.log("变化了", newVal, oldVal);
// })

//情况四： 监听响应式对象中的某一个属性， 该属性是 对象 类型的，要写成函数式
watch(()=>person.car, (newVal, oldVal) => {
  console.log("变化了", newVal, oldVal);

},{deep:true})

</script>
```

#### 情况五  上述的多个数据

监视上述的多个数据 

```vue
<template>
  <div class="greetings">
    {{ person }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed, watch } from "vue"

let person = reactive({
  name: "tom",
  age: 20,
  car: {
    c1: "大众",
    c2: "奥迪"
  }
})

function change() {
  person.car.c1 +='-'
}


//情况五： 监视上述的多个数据   []形式，入参
watch([()=>person.name, ()=>person.car.c1], (newVal, oldVal) => {
  console.log("变化了", newVal, oldVal);

},{deep:true})

</script>
```

### 【watchEffect】

官网:立即运行一个函数，同时响应式地追踪其依赖，并在依赖更改时重新执行该函数。

1 都能监听响应式数据的变化，不同的是监听数据变化的方式不同
2  watch: 要明确指出监视的数据

3 watchEffect:不用明确指出监视的数据    (函数中用到哪些属性，那就监视哪些属性)

```vue

<template>
  <div class="greetings">
    {{ person }}
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person234">
import { ref, reactive, toRefs, toRef, computed, watch ,watchEffect} from "vue"
// watchEffect
let person = reactive({
  name: "tom",
  age: 20,
})

function change() {
  person.age ++
}

// 监听副作用  不用指明监听对象  自动追踪
watchEffect(()=>{
  if(person.age >=22){
    console.log("tom22岁了");
  }
})

</script>
```



### 3.7 【标签的ref属性]

如果用于普通 DOM 元素，引用将是元素本身；

如果用于子组件，引用将是子组件的实例。



使用选项式 API，引用将被注册在组件的 `this.$refs` 对象里：

```
<!-- 存储为 this.$refs.p -->
<p ref="p">hello</p>
```

使用组合式 API，引用将存储在与名字匹配的 ref 里：

```vue
<template>
  <p ref="p">hello</p>
</template>

<script setup>
import { ref } from 'vue'
const p = ref()

console.log(p.value) //拿到dom节点
</script>


```



**演示父组件使用子组件的值**

子组件

```vue

<template>
  <div class="greetings">
    <div ref="titile">测试</div>
    <br>
    <button @click="change">修改</button>

  </div>
</template>

<script setup lang="ts" name="Person">
import { ref, reactive, toRefs, toRef, computed, watch, watchEffect, defineExpose } from "vue"

// 创建一个 titile2, 用于存储ref标记的内容 
// 变量名字和 dom中 ref的名字 ，保持一致
let titile = ref();
 function change(){
  console.log(titile.value); //拿到dom节点
 }

 
let age = ref(40);
defineExpose( { age:age } ) //defineExpose 给出允许使用的值 （vue2中，父组件可以随便拿）

</script>
```

父组件

```vue
<template>
  <div>
    <HelloWorld1 ref="child11" />
    <button @click="test">获取子数据</button>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue" 
import HelloWorld1 from './components/HelloWorld.vue'
let  child11 = ref();

function test() {
  //  console.log(child11.value);
   console.log(child11.value.age); // 拿值
}
</script>
```





或者 `ref` 可以接收一个函数值，用于对存储引用位置的完全控制：

```
<ChildComponent :ref="(el) => child = el" />
```

关于 ref 注册时机的重要说明：因为 ref 本身是作为渲染函数的结果来创建的，必须等待组件挂载后才能对它进行访问。

`this.$refs` 也是非响应式的，因此你不应该尝试在模板中使用它来进行数据绑定。



### 3.8【props】

父组件 

```vue
传入值
<template>
  <div>
    <!-- 父组件传入值 -->
    <HelloWorld  :list=list />  传值和以前一样
  </div>
</template>

<script lang="ts" setup>
import { reactive } from "vue" 
import HelloWorld from './components/HelloWorld.vue'

// 定义一个接口 对变量进行约束
interface PersonInter {
  name: string
  age: number
}
// 自定义一个数组接口
type PersonArray = Array<PersonInter>

let list = reactive<PersonArray>([
  {
    name: "tom",
    age: 20
  }
])


</script>
```



子组件 HelloWorld  

```vue
接受值
<template>
  <div class="greetings">
    <div>测试 </div>
    <br>
    <p>{{father.list}}</p>
    <!-- <button @click="change">修改</button> -->

  </div>
</template>

<script setup lang="ts" name="Person">
import { defineProps ,withDefaults } from 'vue';
// 定义一个接口 对变量进行约束
interface PersonInter {
  name: string
  age: number
}
// 自定义一个数组接口
type PersonArray = Array<PersonInter>


   // 01.子组件接收父组传过来的值
  // var father =  defineProps(["list"])    //list可以直接在插槽中使用

  // 02 list变量 从props中拿出来
  //  console.log(father.list);

// 03 接收list + 限制类型  defineProps可以接受泛型限制
  // defineProps<{list:PersonArray}>() // 表示接受的list 需要符合接口要求

// 04 接收list + 限制类型 + 指定默认值
  let father = withDefaults(defineProps<{list?:PersonArray}>(),{
    list:()=>[{name:"无",age:0 }]
  })
  // 当父组件没有传值的时候，自己可以默认显示

   另一种写法：
   defineProps({
       name:String,
       content:{
           type:String,
           default:()=>{
               return "默认值"
           }
       }
   })
    
    

// 补充：类似 defineXXX defineProps这种，在vue3中称为宏函数； 意思就是说，不用引入，可以直接使用
</script>
```



### 3.9 [vue2与vue的响应式]

### 3.10生命周期

```vue

<script setup lang="ts" name="Person">
import {onBeforeMount, onMounted,onBeforeUpdate,onUpdated,onBeforeUnmount,onUnmounted } from 'vue';
   
 创建阶段   setup
 挂载阶段   onBeforeMount,  onMounted（※）
 更新阶段   onBeforeUpdate, onUpdated（※）
 销毁阶段   onBeforeUnmount（※）, onUnmounted

 常用的：上述加 ※
</script>

注意点：
01. vue3生命周期和vue2类似。前面加on + xxx；销毁阶段有变动。
02. 使用方式有所不同；并且vue3中，同一个钩子，可以出现多次。
03.同一个钩子，子组件先执行，父组件后执行。 原因是js读取组件，是自上而下，逐一解析的。
```

使用方式：

```vue
import { onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue';

onMounted(()=>{
  console.log("执行了");
})
</script>
```



补充：

Vue2 中的生命周期有以下几个:

beforeCreate: 实例刚被创建, 但还未初始化完成.
created: 实例已经创建完成, 数据观测(data observer) 和 event/watcher 事件配置完成, 但还未挂载(mount)
beforeMount: 组件的挂载即将开始, 模板编译还没有开始
mounted: 组件已经挂载完成
beforeUpdate: 组件数据更新前
updated: 组件数据更新后
beforeDestroy: 组件销毁前
destroyed: 组件销毁后



### 3.10 自定义hook

设计理念:

setup中可以写数据和方法，根据功能可以把一类的 methods 和data放到一起。功能较多时，不免阅读麻烦。

所以，是否可以把相同功能的代码，拆分出来，单独放到一个js文件中。类似 mix混入的效果。

这就是hook的功能。

举例： 商品中一个总价显示的功能拆分

src/hooks/useSum.ts

```javascript
import { ref, onMounted } from "vue"
export default function () {
    //数据
    let sum = ref(0)

    //方法
    function add() {
        sum.value += 1
    }

    // hooks文件中，可以使用钩子等方法
    onMounted(() => {
        sum.value = 50  //调用hooks时，把sum初始值，修改为50
    })
    //暴露出去 方法和属性
    return { sum, add }
}

```

组件中使用

```vue
<template>
  <div class="greetings">
    <div>测试 {{sum}} </div>
    <br>

  </div>
</template>

<script setup lang="ts" name="Person">
import { onMounted,  } from 'vue';

import  useSum from "@/hooks/useSum"    引入
 let { sum, add } = useSum();       // 执行一次，获取方法和属性

onMounted(()=>{
  console.log("执行了");

  add();// +1
  add();  //+1   使用
})
```

这样，根据需要，那个组件使用，直接引入即可。  hooks默认指以 usexxx开头，保持这个写法。



### 3.11 Vue2 与Vue3的响应式

**vue2**

```
通过 Object.defineProperty 遍历对象的每一个属性，把每一个属性变成一个 getter 和 setter 函数，读取属性的时候调用 getter，给属性赋值的时候就会调用 setter

对象类型:通过0bject.defineProperty()对属性的读取、修改进行拦截(数据劫持)数组类型:通过重写更新数组的一系列方法来实现拦截。(对数组的变更方法进行了包裹)。
```

**vue3**

```
Proxy 对象用于创建一个对象的代理，从而实现基本操作的拦截和自定义（如属性查找、赋值、枚举、函数调用等）。
```

```
new Proxy(data,{
  //拦截读取属性值
  get(target, prop){
    return Reflect.get(target, prop)
  },
  //拦截设置属性值或添加新属性
  set(target, prop, value){
    return Reflect.set(target, prop, value)
  },
  //拦截删除属性
  deleteProperty(target, prop){
    return Reflect.deleteProperty(target, prop)
  }
})

```





## 4.路由

#### 使用演示

```
npm i vue-router
```

创建路由文件

src/router/index.ts

```tsx
// 创建一个路由器，并暴露出去

// 第一步 引入 createRouter
import { createRouter , createWebHistory } from 'vue-router'

// 引入一个个组件
import Home from "@/pages/Home.vue"
import News from "@/pages/News.vue"

// 第二步 创建路由器
const router = createRouter({
    history:createWebHistory(), //路由模式
    routes:[]
})

export default router
```

main.js中使用

```tsx
import './assets/main.css'

import { createApp } from 'vue'
import App from './App.vue'

import router from "./router"
createApp(App).use(router).mount('#app')

//createApp(App)后，use一下 router.然后在挂载节点
```

App.vue中放置一个路由视口

```vue

<template>
  <div>
   <head>路由测试 head</head>
    <div>
      <a href="/home">home页</a>
      <a href="news">news页</a>
     <br>
     <!-- 官方标签 -->
     <RouterLink to="/home" active-class="active1">*home页</RouterLink>
     <RouterLink :to="{path:'/news'}" active-class="active1">*news页</RouterLink>

    </div>
     <p>展示区</p>
     <div>
       <RouterView/> <----使用标签
     </div>
  </div>
</template>

<script lang="ts" setup>
import {  } from "vue" 
import { RouterView } from "vue-router" <----引入标签

</script>

<style scoped></style>
```

#### 路由模式

1. history 模式

优点: URL更加美观，不带有#，更接近传统的网站URL。
缺点:后期项目上线，需要服务端配合处理路径问题，否则刷新会有 404 错误。

```
const router = createRouter({
    history:createWebHistory(), //路由模式
```



2. hash 模式

优点:兼容性更好，因为不需要服务器端处理路径。
缺点: URL 带有 #不太美观，且在 SE0 优化方面相对较差。

```
const router = createRouter({
history:createWebHashHistory(), //hash模式
    
```

#### RouterLink

```vue
两种写法

<RouterLink to="/home" active-class="active1">*home页</RouterLink>
<RouterLink :to="{path:'/news'}" active-class="active1">*news页</RouterLink>
```

#### 命名路由

作用： 为路由起个名字后，可以多一个跳转页面的方式

```vue
routes:[
        {path:"/home",component:Home ,name:"shouye"},   <---- 重点
        {path:"/news",component:News },
    ]
})
```

后面跳转可以使用如下

```vue
<RouterLink to="/home" >*home页</RouterLink>

<RouterLink :to="{name:'shouye'}" >shouye 页</RouterLink>   <---- 重点
                                                                 
<RouterLink :to="{path:'/news'}" active-class="active1">*news页</RouterLink>
```

嵌套路由

router.js

```vue

   {
            path: "/news",
            component: News,
            children: [{
                path: "detail",
                component:Detail
            }]
        },

```

news页面

```vue
<template>
  <div>
    <div>news页</div>
    <RouterView /> 
  </div>
</template>

<script setup lang="ts" name="Person">
import { RouterView  } from 'vue-router';  <--预留detail组件的显示位置

</script>
```

#### 路由传参

五种传参参考 [](https://www.jb51.net/article/282170.htm)



##### query参数

###### 声明式路由

?号传参

```vue

<RouterLink to="/news/detail?name=tom" >显示详情</RouterLink>
 <RouterLink :to="{ 
      name: 'detail',
      query:{
        title:'测试'
      }

   }" >显示详情</RouterLink>
```

变化点：在页面接受端  因为没有this 了

```vue
<template>
  <div class="greetings">
    <div>news页的详情</div>
    <br>
      {{route.query.name }}
  </div>
</template>

<script setup lang="ts" >

import { useRoute } from "vue-router"
    
let route  = useRoute()   // hooks方法
console.log(route.query);
</script>
```

###### 编程式导航的传参

news页面

```vue
<script setup lang="ts" name="Person">

import {  useRouter } from 'vue-router';
let router  = useRouter()

点击跳转方法
function jump(){
  router.push({
    name:"detail",
    query:{
      titile:"我是编程导航"
    }
  })
}

</script>
```

detail页面

```vue
<script setup lang="ts" >

import { useRoute } from "vue-router"

let router  = useRoute()

console.log(router.query);
</script>
```

注意点：涉及到路由跳转的使用 **useRouter**

​                   涉及到拿参数的使用 **useRoute**

​                                                                                 这两个是不一样的



##### params传参

```js
 {
            path: "/news",
            component: News,
            children: [{
                path: "detail/:name",
                component:Detail
            }]
```

new页面

```vue
  
<RouterLink to="/news/detail/tom" >显示详情</RouterLink>

```

detail页面

```vue
<script setup lang="ts" >

import { useRoute } from "vue-router"
let route  = useRoute()

console.log(route.params);  //{ name: "tom" }
</script>
```



备注1:传递 params 参数时，若使用 to 的对象写法，必须使用 name 配置项，不能用 path。



##### props配置

作用:让路由组件更方便的收到参数(可以将路由参数作为props传给组件)

```js
 {
            path: "/news",
            component: News,
            children: [{
                path: "detail",
                name:'detail',
                component:Detail,
                
//1.props的对象写法，作用:把对象中的每一组key-value作为props传给Detail组件
// props:{a:1.b:2.c:3},
//2.props的布尔值写法，作用:把收到了每一组params参数，作为props传给Detai1组
// props:true
// 3.props的函数写法，作用:把返回的对象中每一组key-value作为props传给Detai1组件                
                props(route){
                    return route.query
                }
            }]
        },
```

news页面

```vue
   <RouterLink :to="{ 
      name: 'detail',
      query:{
        title:'测试'
      },
   }" >显示详情</RouterLink>
```



Detail页面 

```vue
<script setup lang="ts" >
import { defineProps } from "vue"
let data =  defineProps(["title"]) 

console.log(data);
</script>
```





replace属性



编程式路由

```vue
<script lang="ts" setup>
import { onMounted  } from "vue" 
import { useRouter } from "vue-router"
    
const router = useRouter()

onMounted(()=>{
    
  router.push('/news')   // 进入页面后，自动切换页面到news去
})
</script>
```



路由重定向

```
{
path:"/",
redirect:"/home"
}
```



## 5. pinia 菠萝 

https://api.uomg.com/api/rand.qinghua?format=json  获取一句土味情话

nanoid 自动生成唯一id



设计理念：vue2中只有一个store,  vue3中使用pinia， 允许你以功能划分，创建多个store. 因为可以创建多个，所以，在创建过程中，命名应有意义。hooks命名   use + 文件名或功能名 + store  

### 5.1【搭建pinia环境】

引入

```
npm i pinia
```

main.ts

```tsx

import { createApp } from 'vue'
import App from './App.vue'
// 引入pinia
import { createPinia } from "pinia" // 解构出来  1
const pinia = createPinia() // 初始化 2

const  app = createApp(App)

app.use(router)
app.use(pinia)  // 使用pinia  3

app.mount('#app')

```

浏览器上 vue开发工具可以看到一个  菠萝  



### 5.2【存储+读取数据】state

案例：项目中使用了一个计算商品数的功能。sum放到store中，托管，供各个页面使用。

src/store/count.ts

```tsx
// 01 解构定义store的方法
import { defineStore } from "pinia"; 
// 02 创建store       
//  方法命名使用hooks写法            为store变量空间命名一个有意义且唯一的名字
export const useCountStore = defineStore("count", {
    // data数据
    state() {
        return {
            sum: 100
        }
    }
})
```

组件使用

```vue

<template>
  <div class="greetings">
    <div>news页的详情</div>
    <br>
   <h2>当前求和为{{ countStore.sum }}</h2>   两种取值方式  一般直接使用 简单
   <h2>当前求和为{{ countStore.$state.sum }}</h2>
  </div>
</template>

<script setup lang="ts" >

import { useCountStore } from '@/store/count'; // 引入count.ts

const countStore = useCountStore()  // hooks执行一次   vue开发工具上就可以看到
console.log(countStore);

</script>
```







### 5.3【修改数据（三种方式）actions】

store

```tsx
// 01 解构定义store的方法
import { defineStore } from "pinia";
// 02 创建store       
//  方法命名使用hooks写法            为store变量空间命名一个有意义且唯一的名字
export const useCountStore = defineStore("count", {
    // data数据
    state() {
        return {
            sum: 100,
            name: "tom"
        }
    },
    actions: {
        // 对于静态的逻辑可以放到这里
        sumAdd(value:any) {
            console.log("sumadd调用了", value);

            this.sum += value   // this在这里指 useCountStore本身
        }

    }


})
```

使用页面

```vue
<template>
  <div class="greetings">
    <div>store取值页面</div>
    <br>
    <h2>当前求和为{{ countStore.sum }}</h2>
    <h2>当前求和为{{ countStore.$state.name }}</h2>
    <button @click="add">修改</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue"
import { useCountStore } from '@/store/count';

const countStore = useCountStore()
console.log(countStore);

let n = ref(1)
// 定义一个方法
function add() {

  // 第一种修改方式     直接修改  单个属性
  // countStore.sum += 1
  // 第二种修改方式     直接修改  批量修改
  // countStore.$patch({
  //   sum:888,
  //   name:"修改了"
  // })

  // 第三种修改方式    调用 store里定义的 action动作函数  

  countStore.sumAdd(n.value)

}

</script>
```









### 5.4【storeToRefs】

 解构响应式数据的的两种方法对比

```vue
<template>
  <div class="greetings">
    <div>store取值页面</div>
    <br>
    <h2>当前求和为{{ sum }}</h2>
    <h2>当前求和为{{ name }}</h2>
    <button @click="add">修改</button>
  </div>
</template>

<script setup lang="ts">
import { ref , toRefs} from "vue"
import { useCountStore } from '@/store/count';
import { storeToRefs } from "pinia";

const countStore = useCountStore()

// 解构响应式数据的的两种方法对比
// 第一种  全部解构   消耗不必要的计算
// const {sum, name} = toRefs(countStore)
// 第二种 pinia提供的方法
const {sum, name} = storeToRefs(countStore)
console.log(storeToRefs(countStore));//只解构store中的data  推荐

// 定义一个方法
function add() {
  countStore.sum += 1
}

</script>
```



### 5.5【getters】计算属性

store 中的计算属性

```tsx

import { defineStore } from "pinia";

export const useCountStore = defineStore("count", {
    state() {
        return {
            sum: 100,
            name: "tom"
        }
    },
    actions: {
        // 对于静态的逻辑可以放到这里
        sumAdd(value:any) {
            this.sum += value
        }

    },
    // store 中的计算属性
    getters:{
        // state是形参  bigSub计算属性只读
        bigSub(state):Number{
            console.log(this.sum);// this 这里指代useCountStore本身 也可以使用this
           return state.sum*10
        }
    }

})
```

使用页面

```
可以解构出来 直接使用   但是注意：计算属性 只读
const {sum, name,bigSub} = storeToRefs(countStore)

```



### 5.6【$subscribe】

 订阅；相当于watch作用。

类似于 Vuex 的 [subscribe 方法](https://vuex.vuejs.org/zh/api/index.html#subscribe)，你可以通过 store 的 `$subscribe()` 方法侦听 state 及其变化。比起普通的 `watch()`，使用 `$subscribe()` 的好处是 *subscriptions* 在 *patch* 后只触发一次

 ```vue
<script setup lang="ts">
import { useCountStore } from '@/store/count';
import { storeToRefs } from "pinia";

const countStore = useCountStore()
const {sum, name,bigSub} = storeToRefs(countStore)

// 两个形参： 第一个：mutate事件（那个store触发的，old值 new值等）, 第二个参数  state数据
countStore.$subscribe((mutate,state)=>{
  console.log("sum变化了",mutate,state.sum );
} )


// 定义一个方法
function add() {
  countStore.sum += 1
}

</script>
 ```



### 5.7【store组合式写法】

src/store/count1.ts    配置

```tsx

import { reactive } from "vue";
import { defineStore } from "pinia";
// 组合式写法  （相对于选项式）
export const useCountStore = defineStore("count1", () => {
    const list = reactive({
        name: [1, 2, 3, 4, 5]
    })

    function add() {
        list.name.push(10)
    }

return {list ,add }
})
```

使用页面

```vue
<template>
  <div class="greetings">
    <div>store取值页面</div>
    <br>

    <h2> 使用数据{{ list }}</h2>
    <button @click="pushList">修改</button>
  </div>
</template>

<script setup lang="ts">
import { useCountStore } from '@/store/count1';
import { storeToRefs } from "pinia";

const countStore = useCountStore()

const {list } = storeToRefs(countStore) // 只解析数据 不解析方法

function pushList(){
  countStore.add()  // countStore上读取方法使用  (不管是组合还是选项式store.调用里面的方法都是这样)
}

</script>
```













## 6.组件通信

### 6.1 props

​        子   传 父  ：  传数据

​       父    传   子：  传方法     子组件调用的时候，传入参数

父组件

```vue
<template>
  <div class="greetings">
    <div>父页面</div>
    {{car  }}

   这是来自子的数据 --> {{toy  }}
    <br>
     <Child :car="car" :sendToy="getToy"></Child>   
  </div>
</template>

<script setup lang="ts" >
import Child from './Child.vue';
import { ref } from 'vue';

let car = ref("父级数据")
let toy = ref("")
// 方法
function getToy(params:string) {
  toy.value = params
}


</script>
```

子组件

```vue
<template>
  <div class="greetings">
    <div>子页面</div>
    <br>
    这个是 父传子的数据  --》{{car }} <br> 
    <button @click="sendToy(toy)">发送给父级数据</button>
    <button @click="send">发送给父级数据</button>
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps } from 'vue';

let toy = ref("这是子数据")

 var props = defineProps(['car', 'sendToy'])
// 第一种： 模板里直接调用

// 第二种 如下：读出方法 调用

function send(){
  props.sendToy(toy.value)
}

</script>
```

### 6.2 自定义事件 （没有测试成功）emit()

父组件

```vue
<!-- 自定义事件 -->
<template>
  <div class="child">
    <div>父页面8</div>
    {{toy  }}

    <br>
     <Child :car="car" :send-toy="getToy"></Child>   
  </div>
</template>

<script setup lang="ts" >
import Child from './Child.vue';
import { ref } from 'vue';

let car = ref("父级数据")
let toy = ref("000")
// 方法
function getToy(params:string) {
  console.log(params,"收到传值");
  toy.value = params
}

</script>
```

子组件

```vue
<!-- 自定义事件 -->

<template>
  <div class="father">
    <div>子页面899</div>
    <br>
    {{ toy }}
    <button @click="emit('send-toy',toy)">发送给父级数据</button>
  </div>
</template>

<script setup lang="ts">
import { ref, defineEmits } from 'vue';

let toy = ref("子数据")
const emit = defineEmits(["send-toy"])   //defineEmits可以省略  宏函数
</script>
```



### 6.3 mitt

相似概念   ：    作用   **跨组件通信**

1.  pubsub 订阅者
2. $bus  信息总线    应用于vue2
3. mitt    事件总线

接受数据： 提前绑定好事件 （提前订阅消息）

提供数据：在合适的时候触发事件

 on: 开启订阅事件

off： 结束订阅

案例：mitt的使用

```
npm i mitt
```

src/utils/emitter.ts 文件

```tsx

// 第一步 引入mitt
import mitt from 'mitt'
// 第二步  调用mitt得到emitter，emitter 能:绑定事件、触发事件
const emitter = mitt();

// 绑定事件  给事件起个名字  numChange 
emitter.on("numChange1",()=>{
     console.log("发现numChange1 有变化");
})
emitter.on("numChange2",()=>{
     console.log("发现numChange2 有变化");
})

// 触发事件    要触发的事件名字  第二个参数：顺便传个参数
setInterval(()=>{
    emitter.emit('numChange1',10)   // 触发事件并传参
    emitter.emit('numChange2',10)

},1000)


setTimeout(()=>{
    // emitter.off("numChange1") // 取消订阅
    // emitter.off("numChange2") 

    emitter.all.clear()  // 取消所有订阅
},2000)

// 暴漏出去emitter
export default emitter;
```

在组件中的应用

举例：   父组件中，包含两个子组件；  child1,child2.   两个孩子需要通讯。这个时候，子组件

child1.vue

```vue
<!-- 发布消息 -->
<template>
  <div class="father">
    <div>子组件1</div>
    <br>
    <button @click="emitter.emit('send-toy','我是消息')">发布消息</button>  <-----发布消息 
  </div>
</template>

<script setup lang="ts">
import { ref, defineEmits } from 'vue';
import emitter from '@/utils/emitter';   <-----引入 emitter

</script>
```



child2

```vue
<!-- 订阅消息 -->

<template>
  <div class="father">
    <div>子组件2</div>
    <br>
  </div>
</template>
<script setup lang="ts">
import emitter from '@/utils/emitter';

emitter.on('send-toy',value =>{
  console.log("child2接收到了",value );
})


</script>
```

### 6.4  v-model

实际开发中，不适用。   这种在ui组件中，大量使用。





### 6.5  $attrs

1.概述: Sattrs用于实现当前组件的父组件，向当前组件的子组件通信(祖一孙)

2.具体说明: Sattrs 是一个对象，包含所有父组件传入的标签属性。



！！注意: $attrs 会自动排除 props 中声明的属性(可以认为声明过的 props 被子组件自己“消费”了)

父组件

```vue
  
  <Child1 a="aaa" v-bind="{x:10,y:20}" :getToy="getToy"></Child1> 
  
v-bind 对象写法，等同于 k-vale 一个一个写上  传参
```



子组件

```vue
 <Sun v-bind="$attrs"></Sun>

组件穿过来值 都在$attrs上   这句代码表示，来自父组件所有的属性和方法，一股脑给都孙组件
```

孙组件

```vue
孙组件 可以使用变量， 也可以使用传来的方法， 和传入值。
<template>
  <div class="father">
    <div>孙子组件2</div>
    <br>
    {{ x }}
    {{ a }}
    <button @click="getToy(1)">点击增加</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
defineProps(["x","a","getToy"])


</script>
```







### 6.6    $refs ,  $parent

1 .概述：

 ```
$refs 用于 ：  父 -> 子
$parent 用于   父 <- 子
 ```

2. 原理

```
Srefs     值为对象，包含所有被 ref 属性标识的 DOM 元素或组件实例。
Sparent   值为对象，当前组件的父组件实例对象。
```

##### 案例：  父 -> 子 

父组件使用子组件的数据和方法

子组件 

```vue
定义一个数据，交出去。
<template>
  <div class="father">
    <div>子组件1</div>
    <br>
    <p>值{{  childNum }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref, defineEmits } from 'vue';

let childNum = ref(10)

// 把数据交给外部
defineExpose({ childNum })


</script>
```



父组件

```vue
父组件的dom事件，
@click="print($event)"   获取的是事件对象
@click="print($refs)"   获取所有子组件实例对象
<template>
  <div class="child">
    <div>父页面8</div>
    {{ toy }}

    <br>
    <Child1 ref="c1"></Child1>
    <br>
    <Child2 ref="c2"></Child2>
        <!--1. 获取事件对象 -->
    <!-- <button @click="print($event)">打印child1</button>  -->

        <!-- 2.获取所有子组件实例对象 -->
    <button @click="print($refs)">打印child1</button> 
  </div>

</template>

<script setup lang="ts">
import Child1 from './Child1.vue';
import Child2 from './Child2.vue';

import { ref } from 'vue';

let c1 = ref();
let c2 = ref();

// { [key:string]:any }  表示：确定key是字符串  但是字符串中可能是any任意东西
function print(refs:{ [key:string]:any } ) {  
  // event:{c1,c2}获取所有子组件实例对象 可以在这里统一处理 子组件中的数据

   for(let k in refs){
      console.log(refs[k]);
   }
// console.log(c1.value);
// console.log(c2.value);
// c1.value.childNum = 999   // 获取ref数据后，可以随意修改
}

</script>
```

##### 案例： 子  ->   父

子组件使用父组件的数据和方法

父组件

```tsx
<script setup lang="ts">
    
import Child1 from './Child1.vue';
import Child2 from './Child2.vue';
import { ref } from 'vue';

let fatherName = ref("我是父亲")
    
function Child(){
  alert(0)
}


// 把数据交给外部
defineExpose({ Child,fatherName })

</script>
```

子组件

```vue
 关键点：  @click="update( $parent )"  //事件形参传$parent 得到的就是父组件实例对象

<template>
  <div class="father">
    <div>子组件1</div>
    <br>
    <p>值{{  childNum }}</p>
    <button @click="update( $parent )">修改父组件数据</button>
  </div>
</template>

<script setup lang="ts">
import { ref, defineEmits } from 'vue';


function update(parent){
    
 console.log(parent.fatherName);  //调用父组件的属性
parent.Child()   //调用父组件的方法 
 
}


</script>
```



### 6.7 provide  inject

provide  提供    inject注入

父组件：通过provide方法，向后台提供数据和方法；

后台组件，通过inject方法，获取数据和方法。 并且执行方法时，也可以传入参数。达到通讯的目的。



父组件

```vue
<!-- 自定义事件 -->

<template>
  <div class="child">
    <div>父页面</div>
    {{ money }}
    <br>
    {{ num }}
    <Child1></Child1>
    <button @click="add">点击增加</button>
  </div>
</template>

<script setup lang="ts">

import Child1 from './Child1.vue';

import { ref, reactive, provide } from 'vue';

let money = ref(100889999)
let car = reactive({
  brand: "奔驰",
  price: 100
})
function add(){
  money.value+= 1
}

// provide("命名"，值)
provide('qian',money)
provide('che',car)

// 提供方法
let num = ref(10)
function updateNum( n:number ){
  num.value += n
}
provide("moneyContext",{num, updateNum})


</script>
```

后台组件/ 孙组件等

```vue
<template>
  <div class="father">
    <div>孙子组件2</div>
    <br>
    {{ money }} <br>
    {{ car }}
    <button @click="updateNum(1)">点击增加num</button>
  </div>
</template>

<script setup lang="ts">
import { ref ,inject } from 'vue';


// inject 注入    使用数据
// let money = inject("qian");  // 印出来 money变量可以直接使用
// let car = inject("che"); 
  
// 特殊情况  如果没有前面组件提供数据 又可以获取 undefined；
// 这个时候可以使用默认值
let money = inject("qian1","我是默认值"); 
let car = inject("che1",{brand:'未知车辆',price:0})

// 使用方法      和没有获取时的 默认处理
let {num, updateNum } = inject("moneyContext", {num:0,updateNum:(param:number)=>{} })


</script>
```

### 6.8 slot插槽

在使用组件的时候，组件标签中间，可以夹带dom标签。 子组件通过 slot占位标签，标记显示位置。

  使用场景：对于多个ui快，存在样式基本相似，相同位置有小变化的。可以使用插槽。

##### 默认插槽

案例：

父组件

```vue
<template>
  <div class="greetings">
    <div>父页面</div>
    <Child title="今日美食城市">
      <!-- <h1>插槽111</h1> -->
    </Child>

    <Child title="今日美食城市">   

      <h1>插槽2222</h1>  // 插槽内容
    </Child>

  </div>
</template>
<script setup lang="ts">
import Child from './Child.vue';
</script>
```

子组件

```vue
<template>
  <div class="slot">
    <div>子页面 标题{{ title }}</div>
    <div>
      <slot>默认显示内容</slot>   // 占位标记  小提示： slot如果两个，插槽内容，也会显示两遍。
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps } from 'vue';
defineProps(["title"])
</script>
```

##### 具名插槽

父页面

```vue
<template>
  <div class="greetings">
    <div>父页面</div>
    <Child title="今日美食城市">


      <template v-slot:down>  给插槽起个名字
        <ul>
          <li>郑州</li>
          <li>上海</li>
          <li>北京</li>
        </ul>
      </template>

       <template #up>    //简写形式
        <h3>今日美食城市</h3>
      </template>

    </Child>


  </div>
</template>
```

子组件

```vue
<template>
  <div class="slot">
    <div>
        
      <slot name="up">默认显示内容</slot>   slot 起个名对 和插槽内容 一 一对应
        
      <slot name="down">默认显示内容</slot>
        
    </div>
  </div>
</template>

<script setup lang="ts"></script>
```



##### 作用域插槽

数据在子那边，但根据数据生成的结构，却由父亲决定。

父页面

```vue
<template>
  <div class="greetings">
    <div>父页面</div>

    <Child>
      <template v-slot="params">  第一种区参方式
        <ol>
          <li v-for="item in params.youxi">{{ item.name }}</li>
        </ol>
      </template>
    </Child>

    <Child>

      <template v-slot="{ youxi }"> 第二种区参方式
        <h1 v-for="item in youxi">{{ item.name }}</h1>
      </template>
    </Child>

  </div>
</template>
```

子页面

```vue
slot标签  逆向传参
<template>
  <div class="slot">
    <div>
      <slot :youxi="games" x="哈哈" y="你好"></slot>

    </div>
  </div>
</template>

<script setup lang="ts">

import { reactive } from 'vue';
let games = reactive([
  { id: 1, name: "英雄联盟" },
  { id: 2, name: "王者荣耀" },
])

</script>
```











### 7 其他 API

#### 7.1 存疑*【shallowRef 与 shallowReactive】

###### shallowRef 

作用:创建一个响应式数据，但只对顶层属性进行响应式处理，

特点:只跟踪引用值的变化，不关心值内部的属性变化。

```vue
<script lang="ts" setup>
import { shallowReactive, shallowRef } from "vue"


let sum = shallowRef(0)

let person = shallowRef({
  age: 10,
  name:"tom"
})

setTimeout(() => {
sum.value  = 50;  //可以修改 

person.value.age  = 88 // 不可以

person.value = {name:"tony",age:100 } //可以
}, 2000);

// person.value 只关系第一层级的变化

</script>
```

应用场景： 后台返回数据层级很多，实际业务只关系整体替换。本方法效率高。

###### shallowReactive

只对顶层属性进行响应式处理

```
let car = shallowReactive({
  barnd: "奔驰",
  options: {
    color: "红色",
    engine: "v8"
  }
})
// 只关系第一层数据改变，更新视图  其他深层 不更新视图
car.barnd   可以修改
car.options  可以修改
```

#### 7.2【readonly与shallowReadonly】

##### readonly 

作用：创建一个对象的深只读副本；浅层，深层，都不能修改。

场景： 保护一个数据，不让随意修改。

```js
let sum = ref(0)

let person = ref({
  age: 10,
  name: "tom"
})

let copySum = readonly(sum) // 入参是一个响应式数据

let copyperson = readonly(person) 

使用方法不能修改；但又关联关系，sum的修改，副本copySum 也会变化。
function test() {
  copyperson.age += 10 // 不可以
}
```

##### shallowReadonly 

作用：和readonly类似；但只限制对象的顶层属性。

浅层不能改，深层可以改。

```vue
let person = reactive({
  age: 10,
  name: "tom",
  hobby:{
    aa:"play"
  }
})

let copySum = shallowReadonly(sum) // 入参是一个响应式数据

let copyperson = shallowReadonly(person) 


function test() {
  copyperson.hobby.aa += 10 // 不可以
}

```

#### 7.3 【toRaw与markRaw 】

##### toRaw

作用:用于获取一个响应式对象的原始对象，toRaw 返回的对象!不再是响应的，不会触发视图更新.

场景： 在需要将响应式对象传递给非 vue 的库或外部系统时，使用 toRaw 可以确保它们收到的是普通对象

```
import { reactive , toRaw } from "vue"
let person = reactive({
  age: 10,
  name: "tom",
  hobby:{
    aa:"play"
  }
})

console.log(toRaw(person)); // 普通对象
```

##### markRaw 

作用:标记一个对象，使其永远不会变成响应式的。

如果一个普通对象，加了markRaw（对象）；那么这个对象，后面，即使加上reactive（）；也不是响应式：

>场景：mockis 模拟数据；第三方库暴漏的对象， 是不需要变成响应式。
>
>例如使用 mockis时，为了防止误把 mockis 变为响应式对象，可以使用 markRaw 去标记 mockjs



```js
import { reactive, ref, shallowReadonly, toRaw, markRaw } from "vue"

// raw adj:未经加工的
let person = markRaw( {
  age: 10,
  name: "tom",
  hobby: {
    aa: "play"
  }
}) 
// let person ={
//   age: 10,
//   name: "tom",
//   hobby: {
//     aa: "play"
//   }
// } 
let person2 = reactive(person);// person2变成响应式数据


function test() {
  person2.age += 10 // 不可以
}
```



#### 7.4 customRef 自定义ref

作用:创建一个自定义的ref，并对其依赖项跟踪和更新触发进行逻辑控制。实现防抖效果(useSumRef.ts)



通过自定义customRef方法，实现，输入框输入后 2s后，页面变化  ；根据场景可以开发其他功能

useMsgRef.ts   

```tsx
import { customRef } from "vue";

//使用vue提供的customRef定义响应式数据
export default function(initValue:string,delay:number){
    let timer:number;
    let msg = customRef( (track, trigger)=>{
        return {
            // get何时调用 msg被读取值的时候
            get() {
                track() //跟踪 高速Vue数据msg很重要，对其进行时许关注
                return initValue
            },
              // set msg被修改的时候
            set(value:string){
                clearTimeout(timer )
                timer = setTimeout(() => { 
                    initValue = value
                    trigger() //触发  通知Vue一下msg变化了
                }, delay);
            }
        }
    })
    return {msg}
```

使用页面

```vue
<template>
  <div>
  
    {{ msg }}
    <input type="text" v-model="msg">

  </div>
</template>

<script lang="ts" setup>

import useMsgRef from "./hooks/useMsgRef";

// 通过自定义customRef方法，实现，输入框输入后 2s后，页面变化  ；根据场景可以开发其他功能
let { msg } = useMsgRef("11",2000)



</script>
```

#### 7.5Teleport 插入指定节点

什么是Teleport?-- Teleport 是一种能够将我们的组件html结构移动到指定位置的技术.

类似与element中的弹窗，当弹窗位置异常的时候，指定弹窗的节点，插入到根节点下。

```vue
<teleport to="body">
  <div class="modal" v-show="isShow">
    <h2>我是一个弹窗</h2>
    <p>内容</p>
    <button @click="isShow = false"></button>
  </div>
</teleport>
```



#### 7.6 Suspense 包裹异步组件



```vue
     <!-- Suspense 用于处理：当自组件中，有异步事件，例如axios请求，
    父组件在加载的时候，子组件滞后显示，造成页面突然显示dom。
    此方法可以加一下过渡效果
    -->
     <Suspense>
      <template v-slot:default>  返回后， 正常显示这个
         <Child></Child>
      </template>
      <template v-slot:fallback>
       <h1>组件加载中。。。。</h1>   // 组件中的数据，未返回是的时候，显示这个
      </template>
     </Suspense>
```















#### app身上的全局API

###### app.component 

注册全局组件

main.ts

```tsx
import { createApp } from 'vue'
import App from './App.vue'

import hello from "./components/HelloWorld.vue"  01

const  app = createApp(App)

app.component('hello',hello) //注册全局组件  02

app.use(router)
app.mount('#app')
```

任意组件使用

```tsx
<template>
  <div>
  
            <hello></hello>  03

  </div>
</template>
```

###### app.config

```vue
原来
vue2
  Vue.prototype.$path =  = '/api/'
    main.ts
vue3
app.config.globalProperties.$path  = '/api/'
```

任意组件

```vue
<template>
  <div>
     {{ $path }}
  </div>
</template>
```

注意点： ts文件中使用，如果报红。则定义一下接口类型

```
main.ts文件中

declare modules "vue"{
    interface ComponentcustomProperties {
        $path:"string"     <---- 把你定义的全局变量， 生命一下
    }
}
```



###### app.derective

注册全局指令

```
main.ts

app.directive("beauty", (element, { value }) => {
    element.innerText += value;
    element.style.color = "green"
})
```

任意组件使用

```
并传值
<p v-beauty="'添加文字'">88</p>
```

详见10小结



###### app.mount

```
main.ts
   挂载节点
app.mount('#app')
```



###### app.unmount

```vue
main.ts
   卸载节点
   
 .....  
app.use(router)
app.use(pinia)

app.mount('#app')

setTimeout(() => {
    app.unmount()    2s后，卸载应用
}, 2000);
```

###### app.use

安装插件时使用

```
app.use(pinia)
```

### 8 使用路由 视口标签

(注意：插件和vue2的是不一样的)

```
npm install vue-router@4.0.0-beta.13

```

router.js稍作改造

```
import Vue from 'vue'

import { createRouter, createWebHistory } from 'vue-router'

const routerHistory = createWebHistory() //

import test from '@/views/test.vue'

export default createRouter({
  history: routerHistory,
  routes: [
    {
      path: '/',
      name: 'test',
      component: test
    }
  ]
})

```

main.js稍作改造

```
import { createApp } from 'vue';
import App from './App.vue'

import router from './router'

createApp(App).use(router).mount('#app')
```

app组件放置 组件视口标签

```
<router-view></router-view>
```

## 9.vue的内置组件

### 01  component 组件

https://blog.csdn.net/weixin_52203618/article/details/127683606

 <component>是一个内置组件，is是固定的属性，依赖 "is" 的值来决定渲染哪一个组件；现在来通过对以上代码的一个修改！

```
<div id="app">
    
    <header>
        <ul>
            <li v-for="item in nav" :key="item.id" @click="handChange(item)" :class="isChoose == item.id?'active':''">{{item.title}}</li>
        </ul>
    </header>
 
    <component :is="isChoose"></component>
 
</div>
<script>
    Vue.component("home",{
        template:`
            <div style="padding:10px">
                / 首页   
            </div>
        `
    })
 
    Vue.component("server",{
        template:`
            <div style="padding:10px">
                / 服务    
            </div>
        `
    })
 
    Vue.component("about",{
        template:`
            <div style="padding:10px">
                / 关于
            </div>
        `
    })
 
    new Vue({
        el:'#app',
        data:{
            nav:[{title:'首页',id:'home'},{title:'服务',id:'server'},{title:'关于',id:'about'}],
            isChoose: 'home'  
        },
        methods:{
            handChange(item){
                // console.log(item);
                this.isChoose = item.id
            }
        }
    })
</script>
```

### 02.[slot](https://v2.cn.vuejs.org/v2/api/#slot)

https://v2.cn.vuejs.org/v2/api/#slot

- **Props**：

  - `name` - string，用于命名插槽。

- **Usage**：

  `<slot>` 元素作为组件模板之中的内容分发插槽。`<slot>` 元素自身将被替换。

### 03.[keep-alive](https://v2.cn.vuejs.org/v2/api/#keep-alive)

[keep-alive](https://v2.cn.vuejs.org/v2/api/#keep-alive)

- **Props**：

  - `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存。
  - `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
  - `max` - 数字。最多可以缓存多少组件实例。

- **用法**：

  `<keep-alive>` 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 `<transition>` 相似，`<keep-alive>` 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在组件的父组件链中。

  当组件在 `<keep-alive>` 内被切换，它的 `activated` 和 `deactivated` 这两个生命周期钩子函数将会被对应执行。

```
<!-- 基本 -->
<keep-alive>
  <component :is="view"></component>
</keep-alive>

<!-- 多个条件判断的子组件 -->
<keep-alive>
  <comp-a v-if="a > 1"></comp-a>
  <comp-b v-else></comp-b>
</keep-alive>

<!-- 和 `<transition>` 一起使用 -->
<transition>
  <keep-alive>
    <component :is="view"></component>
  </keep-alive>
</transition>
```

### 04 .[transition](https://v2.cn.vuejs.org/v2/api/#transition)

[过渡：进入，离开和列表](https://v2.cn.vuejs.org/v2/guide/transitions.html)

### 05 TransitionGroup

[官网详解](https://cn.vuejs.org/guide/built-ins/transition-group.html#transitiongroup)

`<TransitionGroup>` 是一个内置组件，用于对 `v-for` 列表中的元素或组件的插入、移除和顺序改变添加动画效果。







### 使用场景：vue组件缓存与动画效果

https://blog.csdn.net/m0_71933813/article/details/129542249

```vue
<section class="app-main">
    <router-view v-slot="{ Component, route }">
      <transition name="fade-transform" mode="out-in">
        <keep-alive :include="tagsViewStore.cachedViews">
          <component v-if="!route.meta.link" :is="Component" :key="route.path"/>
        </keep-alive>
      </transition>
    </router-view>
    <iframe-toggle />
  </section>
```

  

主要是利用了[router-view](https://so.csdn.net/so/search?q=router-view&spm=1001.2101.3001.7020)组件的插槽来实现，使用<transition>和<keep-alive>组件来包裹路由组件

 <component :is="Component" :key="route.path"/>

主要是利用了router-view组件的插槽来实现，使用<transition>和<keep-alive>组件来包裹路由组件

注解：

<router-view> v-slot Component是router-view要显示的组件对象 route路由是什么

<transition>name定义要过度的动画效果也就是css样式

<transition>mode过渡模式（执行的顺序）先进来在出去

<keep-alive> max缓存组件数量，限定缓存5

<component>is动态渲染组件 判断条件如果为真就渲染组件
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/m0_71933813/article/details/129542249

## 10 vue3的自定义指令

​	[Vue3自定义指令directives介绍](https://blog.csdn.net/weixin_43953518/article/details/133750117?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-133750117-blog-135869094.235^v43^pc_blog_bottom_relevance_base8&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

指令是带有 v- 前缀的特殊 attribute。[Vue](https://so.csdn.net/so/search?q=Vue&spm=1001.2101.3001.7020) 提供了许多内置指令，例如：v-bind、v-html等。

我们可以创建自己想要的指令，使用必须以`v-`为前缀

##### **分类**

局部指令：组件中通过`directives`选项实现，只能在当前组件中使用
全局指令：应用实例的`directive`方法，可以在任意组件中被使用（所有内置指令都为全局指令）

自定义指令跟组件一样，也是有生命周期的，下面看一下他的生命周期

生命周期介绍
created：在绑定元素的 attribute 或事件监听器被应用之前调用；
beforeMount：当指令第一次绑定到元素并且在挂载父组件之前调用；
mounted：在绑定元素的父组件被挂载后调用，大部分自定义指令都写在这里；
beforeUpdate：在更新包含组件的 VNode 之前调用；
updated：在包含组件的 VNode 及其子组件的 VNode 更新后调用；
beforeUnmount：在卸载绑定元素的父组件之前调用；
unmounted：当指令与元素解除绑定且父组件已卸载时，只调用一次；
钩子参数介绍
每个钩子函数中有回调参数，回调参数有四个，含义基本上和 Vue2 一致：

el：指令所绑定的元素，可以用来直接操作 DOM（可以进行事件绑定）。
binding：我们通过自定义指令传递的各种参数
vnode：Vue 编译生成的虚拟节点。
oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用
binding包含以下属性

value：传递给指令的值。例如在 v-my-directive=“1 + 1” 中，值是 2。
oldValue：之前的值，仅在 beforeUpdate 和 updated 中可用。无论值是否更改，它都可用。
arg：传递给指令的参数 (如果有的话)。例如在 v-my-directive:foo 中，参数是 “foo”。
modifiers：一个包含修饰符的对象 (如果有的话)。例如在 v-my-directive.foo.bar 中，修饰符对象是 { foo: true, bar: true }。
instance：使用该指令的组件实例。
dir：指令的定义对象。

**指令的钩子**

```
const myDirective = {
  // 在绑定元素的 attribute 前
  // 或事件监听器应用前调用
  created(el, binding, vnode, prevVnode) {
    // 下面会介绍各个参数的细节
  },
  // 在元素被插入到 DOM 前调用
  beforeMount() {},
  // 在绑定元素的父组件
  // 及他自己的所有子节点都挂载完成后调用
  mounted() {},
  // 绑定元素的父组件更新前调用
  beforeUpdate() {},
  // 在绑定元素的父组件
  // 及他自己的所有子节点都更新后调用
  updated() {},
  // 绑定元素的父组件卸载前调用
  beforeUnmount() {},
  // 绑定元素的父组件卸载后调用
  unmounted() {}
}

```

##### 指令的使用

简单需求： 当某个元素挂载完成后可以自动获取焦点

默认的实现方式，假如有多个地方需要使用时，这种实现方式的代码会显得繁杂冗余

```vue
<template>
  <div>
    <input type="text" ref="input" />
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup () {
    const input = ref(null);

    onMounted(() => {
      input.value.focus();
    })

    return {
      input
    }
  }
}
</script>

<style scoped>
</style>


```

**使用自定义指令实现**

```vue
<template>
  <input type="text" v-focus />
</template>
<script setup>
// 在模板中启用 v-focus
const vFocus = {
  mounted: (el) => el.focus()
}
</script>

```

注：在`<script setup>` 中，任何以 `v` 开头的驼峰式命名的变量都可以被用作一个自定义指令，`vFocus` 即可以在模板中以 `v-focus` 的形式使用

如果不使用 `<script setup>`，自定义指令可以通过 `directives` 选项注册

```vue
<template>
  <input type="text" v-focus />
</template>
<script>
export default {
  setup() {
    /*...*/
  },
  directives: {
    focus: {
       mounted: (el) => el.focus()
    }
  }
}
</script>

```

也可以全局注册该指令，这样所有组件都可以使用`v-focus`

```vue
const app = createApp({})

// 使 v-focus 在所有组件中都可用
app.directive('focus', {
 	mounted: (el) => el.focus()
})

```

##### 指令的参数和修饰符

假如我们使用这样一个指令`v-example`

```
<div v-example:params.lazy="someValue"></div>

```

此时指令钩子函数的binding 参数会是一个这样的对象：

```vue
{
  arg: 'params',
  modifiers: { lazy: true },
  value: /* `someValue` 的值 */,
  oldValue: /* 上一次更新时 `someValue` 的值 */
}

```

也就是说指令`:`后面跟着的是指令的参数，`.`后面跟着的是指令的修饰符

示例：背景高亮

```vue
<template>
  <div>
    <div v-highlight>默认的高亮颜色</div>
    <div v-highlight="{ bgColor: 'red', color: 'yellow' }">这是一个简单的例子</div>
  </div>
</template>
<script>
export default {
  setup() {
    /*...*/
  },
  directives: {
    highlight: {
      mounted(el, binding) {
        console.log('binding', binding)
        const color = binding.value && binding.value.color ? binding.value.color : '#fff'
        const bgColor = binding.value && binding.value.bgColor ? binding.value.bgColor : 'blue'
        el.style.color = color
        el.style.backgroundColor = bgColor
      }
    }
  }
}
</script>

```

示例2：

```vue
<template>
  <div>
    <div v-letter:uppercase>hello world</div>
  </div>
</template>
<script>
export default {
  setup() {
    /*...*/
  },
  directives: {
    letter: {
      mounted(el, binding) {
        const text = el.innerHTML
        if (binding.arg === 'uppercase') {
          el.innerHTML = text.toUpperCase()
        } else if (binding.arg === 'lowercase') {
          el.innerHTML = text.toLowerCase()
        } else {
          el.innerHTML = text.split('')
        }
      }
    }
  }
}
</script>

```

其他相关：[指令](https://blog.csdn.net/qq_43231248/article/details/135869094)

## 11 vue3的getCurrentInstance获取组件实例踩坑记录

一、getCurrentInstance基本用法
我们可以通过 getCurrentInstance这个函数来返回当前组件的实例对象,也就是当前vue这个实例对象
Vue2中，可以通过this来获取当前组件实例；
Vue3中，在setup中无法通过this获取组件实例，console.log(this)打印出来的值是undefined。

在Vue3中，getCurrentInstance()可以用来获取当前组件实例
常见的用途包括：

访问组件实例的属性：可以通过 getCurrentInstance().ctx 或 getCurrentInstance().proxy 来获取当前组件实例的属性。例如，可以使用 getCurrentInstance().ctx.$props 访问组件的 props 属性。

调用组件实例的方法：可以通过 getCurrentInstance().ctx 或 getCurrentInstance().proxy 来调用当前组件实例的方法。例如，可以使用 getCurrentInstance().ctx.$emit 来触发组件的自定义事件。

在生命周期钩子中使用：可以在组件的生命周期钩子中使用 getCurrentInstance() 来获取当前组件实例，以便在钩子函数中访问组件实例的属性或调用组件实例的方法。

请注意，getCurrentInstance 的返回值是一个组件实例对象，可以通过 .ctx 来访问该实例的上下文对象，或者通过 .proxy 来访问该实例的代理对象。两者的区别在于，通过 .ctx 访问的是真实的组件实例，而通过 .proxy 访问的是一个代理对象，该代理对象可以在模板中直接使用。

基本使用：

```vue
import { getCurrentInstance, onMounted} from 'vue'
export default {
    setup() {
        onMounted(() => {
            const instance = getCurrentInstance()
            console.log('实例', instance)
        })
        return {}
     }

```

我们可以根据自己的需求使用当前实例的一些属性和方法，`比如我们获取当前组件中某个div的dom`

代码如下：

```vue
<template>
    <div id="cx-container" :ref="refName">
    </div>
</template>
<script>
import { getCurrentInstance, onMounted} from 'vue'
export default {
    setup() {
        const refName = 'cxContainer'
        onMounted(() => {
            const instance = getCurrentInstance().ctx
            const dom = instance.$refs[refName]
            console.log('dom', dom)
        })
        return {
       		 refName 
        }
     }
</script>

```

**二、getCurrentInstance使用注意点**

**1. getCurrentInstance 只能在 setup 或生命周期钩子中使用**

举个例子：

```vue
<script>
import { getCurrentInstance, onMounted} from 'vue'
export default {
    setup() {
        const refName = 'cxContainer'
        const onResize = () => {
            const instance = getCurrentInstance()
        	console.log('instance', instance)		
        }
        onMounted(() => {
            window.addEventListener('resize', onResize)
        })
        return {
       		 refName 
        }
     }
</script>

```

以上代码我们将`const instance = getCurrentInstance()`放在了`onResize`函数中，然后在`onMounted`中监听浏览器尺寸变化，尺寸变化就出发onResize函数。
**打印结果如下：**



可以看到instance为null,
这时如果我们将const instance = getCurrentInstance()放到setup函数中，或者onMounted中就可以成功获取实例

如需在 setup或生命周期钩子外使用，先在 setup 中调用 getCurrentInstance() 获取该实例然后再使用。


**2 getCurrentInstance**线上环境报错问题**

**本地代码**

```
<script>
    import {getCurrentInstance} from "vue";
    export default {
      setup() {
         const {ctx} = getCurrentInstance();
         console.log('ctx', ctx)
      }
    
</script>

```

以上代码在本地开发调试没有问题，在线上环境会报错，`如果通过这个ctx.$refs[xxx]获取dom，线上就会有问题`。
**解决方案**

> 使用proxy代替ctx,proxy线上不会出现问题

```
const { proxy } = getCurrentInstance()  

```

**三、在vue3中不推荐使用getCurrentInstance获取组件实例**

官方解释：
主要还是 getCurrentInstance 是一个内部的API，并不是公开的API，使用内部API去实现一些业务功能，可能会因为后续 Vue 的版本迭代而造成业务上的 BUG。

至于其他的一些常用属性和方法，vue3中的setup中提供了props和contexts上下文。

[官方setup用法](https://cn.vuejs.org/api/composition-api-setup.html#setup-context)

## 12 setup下的组件name命名插件

在[vue3](https://so.csdn.net/so/search?q=vue3&spm=1001.2101.3001.7020)组合式api中，我们可以如下命名

```vue
<script >
export default
name :  组件名字 ,
setup(){ }
```

这样便可以轻松命名组件，但是我们通常使用setup[语法糖](https://so.csdn.net/so/search?q=语法糖&spm=1001.2101.3001.7020)形式(<script setup>)来写代码，一旦使用语法糖，便不能再使用上述命名方法，以下我统计了一些setup语法糖的组件命名方法

第一种：写两个script标签，一个专门用来命名。

第二种：插件  **unplugin-vue-setup-extend-plus**

1.安装

```
npm i unplugin-vue-setup-extend-plus
```

2.1vit.config.js配置

```vue
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
 
import vueSetupExtend from 'unplugin-vue-setup-extend-plus/vite'
 
export default defineConfig({
  plugins: [vue(),vueSetupExtend({
    enableAutoExpose: true
  })],
})
```

2.2在webpack环境下vue.config.js配置

```vue
module.exports = {
  plugins: [
    require('unplugin-vue-setup-extend-plus/webpack').default({
        enableAutoExpose: true
     })
  ]
}
```

3. 然后就可以在script上随意定义组件名了

   ```
   <script setup name="name</script>
   ```



## 13vue3【vite】中使用cesium

## 本地安装[cesium](https://so.csdn.net/so/search?q=cesium&spm=1001.2101.3001.7020) 

安装vite-plugin-cesium：

```
npm i -D vite-plugin-cesium
```

安装cesium：

```
npm i -S cesium
```

vite.config.js中配置如下：

```
import cesium from 'vite-plugin-cesium';
```

![](https://img-blog.csdnimg.cn/5267ccdfa6f34bf5a6b5e797e425cec0.png)

```vue
<template>
    <div id="cesiumContainer"></div>
  </template>
  
  <script setup>
  import * as Cesium from 'cesium';
  import { onMounted } from 'vue';
  onMounted(() => {
    const viewer = new Cesium.Viewer('cesiumContainer',{
      infoBox: false, // 禁用沙箱，解决控制台报错
    });
  })
  
  </script>
  
  <style scoped>
  #cesiumContainer {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0px;
    left: 0px;
    margin: 0;
    padding: 0;
    overflow: hidden;
  }
  </style>
```







## 其他

```vue
import { 

ref, reactive, toRefs, toRef, computed, watch, watchEffect, defineExpose 

} from "vue"

```

vue3非兼容的变更 

https://www.javascriptc.com/vue3js/guide/migration/introduction.html#%E9%9D%9E%E5%85%BC%E5%AE%B9%E7%9A%84%E5%8F%98%E6%9B%B4







## TS在vue3中的应用

接口

```javascript
interface PersonInter {
  name: string
  age: number
}
// 自定义一个数组接口
type PersonArray = Array<PersonInter>


// 使用接口 -- 约束对象
let person: PersonInter = {
  name: "tom",
  age: 20
}

// 响应式数据 使用接口方式
let list:PersonArray = [
  {
    name: "tom",
    age: 20
  }
]

// 响应式数据 使用接口方式一
let list2:PersonArray = reactive([
  {
    name: "tom",
    age: 20
  }
])
// 响应式数据 使用接口方式二
let list23 = reactive<PersonArray>([
  {
    name: "tom",
    age: 20
  }
])
```













