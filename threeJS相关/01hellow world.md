# threeJS

## 网址

官网： https://threejs.org/

文档： https://threejs.org/manual/#zh/fundamentals

网络自建私网

www.three3d.cn

https://www.three3d.cn/docs/index.html#manual/zh/introduction/Creating-a-scene

学习指南：

https://www.three3d.cn/threejs/01-%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/01-%E5%89%8D%E7%AB%AF3D%E5%8F%AF%E8%A7%86%E5%8C%96Three.js%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF.html

## 简介

Three.Js是基于WebGL的JavaScript开源框架，简言之，就是能够实现3 D效果的JS库。

threejs是一个让用户通过javascript入手进入搭建webgl项目的类库。



![](.\img\1.png)

## Three.js应用场景

利用Three.JS可以制作出很多酷炫的3D动画，并且Three.js还可以通过鼠标、键盘、拖拽等事件形成交互，在页面上增加一些3D动画和3D交互可以产生更好的用户体验。
通过Three.JS可以实现全景视图，这些全景视图应用在房产、家装行业能够带来更直观的视觉体验。在电商行业利用Three.JS可以实现产品的3D效果，这样用户就可以360度全方位地观察商品了，给用户带来更好的购物体验。另外，使用Three.JS还可以制作类似微信跳一跳那样的小游戏。随着技术的发展、基础网络的建设，web3D技术还能得到更广泛的应用。

## 学习路线

### 第一部分： 基础概念

点

线

面

几何体

材质

物体

场景

相机

渲染器

动画

控制器

### 第二部分：运用

二: 搞定一个最基础的场景和 3D 物体的显示
三:详细了解官网文档里上述概念的各类属性和概念。
四:了解什么是 PBR,PBR 基于物理的光照原理的渲染。
五:掌握什么是环境贴图，凹凸贴图放射光，金属贴图，粗糙度贴图等。
六:掌握如何绘制粒子群，来绘制雨雪，落叶，星河等各种粒子效果。

七:实现能和物体进行交互，如何选中与场景中的物体进行交互。
八:掌握物理引擎让物体有真实的物理效果，比如重力，反弹，摩擦力等。
九:掌握着色器语言，控制 GPU 渲染掌握实现 three.js底层封装原理，图形渲染原理。
十:掌握编写顶点着色器和片元着色器，来绘制动态飘摇的旗帜，以及编写动态的烟雾和乌云，水纹。

十一:继续掌握各种后期合成效果，对整个渲染画面进行调整。例如打造闪烁的画面，雪花感的电视画面等
十二:掌握曲线和物体运动的结合，再加上着色器编写，就可以实现各种飞线,雷达和光墙特效。
十三:如果需要掌握渲染精美真实的智慧园区的，还需要掌握建模技术，例如学习 blender 软件。



学习three.js首先掌握基础概念什么是点、线、面、几何体、材质、物体、场景、相机、渲染器、动画、控制器等基础概念，搞定一个最基础的场景和3d物体的显示。接着学会调试3D开发代码。接着即可深入上诉概念的每一个概念，详细了解官网文档该类的各种属性与概念。

接着3d渲染要真实性，肯定离不开PBR，详细了解什么是PBR，PBR基于物理的光照原理的渲染,。掌握什么是环境贴图、凹凸贴图、置换贴图、放射光、,环境贴图、金属贴图、粗糙度贴图等等，去打造真实的物体显示效果。接着掌握如何绘制粒子群，来绘制雨雪、落叶、星河等各种粒子效果，甚至产品的粒子效果。

​     掌握了这些，基本就算入了个小门了，接着就是要实现能和物体进行交互，如何选中与场景中的物体进行交互。而且还要能够掌握物理引擎让物体有真实的物理效果，例如重力，反弹、摩擦力等这样物体相互作用会更加真实。

接着就要开始真正进入WEBGL魔力的世界，掌握着色器语言，控制GPU渲染，掌握实现three.js底层封装的原理，能够图形渲染原理，掌握编写顶点着色器和片元着色器，来绘制动态飘扬的旗帜。以及编写动态的烟雾和乌云，水纹。

掌握了这些就可以写节日酷炫的烟花了，接着可以继续掌握各种后期合成效果，对整个渲染画面进行调整，例如打造闪烁的画面，雪花感的陈旧电视画面，又或者通过编写着色器，打造出水底世界的效果。

接着掌握曲线和物体运动的结合，在加上着色器编写，即可实现各种飞线、雷达、光墙特效。通过地理信息数据，获取建筑信息，可以生成建筑的框架和高度渲染出数字城市。当然日常网页也或有一些文字信息标识，想要文字标识也加上3d效果，就需要掌握css3d的渲染器来渲染。

当然如果需要掌握渲染精美真实的智慧园区的，就需要掌握建模技术，例如学习blender软件搭建模型和优化模型，才能最终输出到网页中，包括动画也可以先用blender做好在输出到网页中，不用辛苦的进行复杂动画的编写，可以可视化的制作。	

## 项目运用

在vue项目中第一个dem。

  作为一个插件使用。

```shell

npm install three  

```



在home.vue页面中

```vue
<template>

</template>
<script setup>
//引入所有核心方法
import * as THREE from "three"
// 创建场景
const scene = new THREE.Scene();
// 创建相机
const camera = new THREE.PerspectiveCamera(
    45, //视角
    window.innerWidth / window.innerHeight, //宽高比
    0.1, //近平面
    1000,//原平面
);

//创建渲染器
const renderer = new THREE.WebGLRenderer();
//要渲染的宽高尺寸
renderer.setSize(window.innerWidth, window.innerHeight);
//将画布 挂载到dom中
document.body.appendChild(renderer.domElement);


// 创建一个几何体
const geometry = new THREE.BoxGeometry(1,1,1);
//创建材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
//创建网格
const cube = new THREE.Mesh(geometry, material);
//将网格添加到场景中
scene.add(cube);
//设置相机的位置
camera.position.z = 5;   //  x y z轴的距离  默认是0
camera.lookAt(0,0,0); // 默认看向原点

// renderer.render(scene, camera);
function animate() {
  requestAnimationFrame(animate);// 关键帧调用  循环调用
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();

window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});



</script>
```



#### 01-坐标辅助器

**AxesHelper**

用于简单模拟3个坐标轴的对象.
红色代表 X 轴. 绿色代表 Y 轴. 蓝色代表 Z 轴.

**代码示例**

```
const axesHelper = new THREE.AxesHelper( 5 );
scene.add( axesHelper );
```

#### 02-轨道控制器查看物体

轨道控制器是three.js中非常实用的一个工具，它可以帮助用户更轻松地探索3D场景。使用轨道控制器，用户可以通过鼠标或触摸屏来旋转、缩放和平移相机，从而改变相机的视角，观察场景中的不同物体或角度。具体来说，轨道控制器可以通过鼠标或触摸屏来旋转相机，改变场景的视角，调整场景的大小，移动场景中的物体。

```
import { OrbitControls } from "three/examples/jsm/controls/orbitControls.js";

//添加轨道控制器
// const controls = new OrbitControls( camera, renderer.domElement );
const controls = new OrbitControls( camera, document.body );
// 设置带阻尼的惯性
controls.enableDamping = true;
//设置阻尼系数
controls.dampingFactor = 0.05;//值越大 阻尼越大 停下的越快

controls.autoRotate = true;  //将其设为true，以自动围绕目标旋转  更多属性查看 类OrbitControls
```

#### 03 物体位移与父子元素

放大和旋转， 父子盒子有牵连关系。  父盒子放大，会使子盒子放大。 旋转亦然。

子盒子放大和旋转，不会影响父盒子。

```

// 创建一个几何体
const geometry = new THREE.BoxGeometry(1,1,1);
//创建材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const father_material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
//创建网格
const father_cube = new THREE.Mesh(geometry, father_material);
const cube = new THREE.Mesh(geometry, material);
cube.position.set(2,0,0)
// 放大3倍
// cube.scale.set(1,1,1);

father_cube.position.set(0,0,0)
// 旋转45度
father_cube.rotation.x = Math.PI / 4;
cube.rotation.x = Math.PI / 4;

father_cube.add(cube);

//将网格添加到场景中
scene.add(father_cube);
```

#### 04 画布自适应窗口变化

当窗口大小发生变化时，我们需要更新Three,js渲染器的视口(viewport)和渲染的画布(canvas)尺寸，以确保我们的场景和对象能够正确地显示。你会发现，如果不适应窗口大小变化，我们前面写好的代码在页面尺寸发生改变的时候，会出现空白或者滚动条突出的情况。因此，我们需要监听屏幕大小的改变，重新设置相机的宽高比例和渲染器的尺寸大小，代码如下:

```
// 设置响应画布
window.addEventListener('resize', () => {
  //更新摄像头的宽高比
  camera.aspect = window.innerWidth / window.innerHeight;
  //更新摄像机的投影矩阵
  camera.updateProjectionMatrix();
  //更新渲染器
  renderer.setSize(window.innerWidth, window.innerHeight);
  //更新渲染器的像素比
  renderer.setPixelRatio(window.devicePixelRatio);
});

```

#### 05 应用Iil-GUI调试开发3D效果

​      模型参数：调试工具方法

```
<template>

</template>
<script setup>
//引入所有核心方法
import * as THREE from "three"
import { OrbitControls } from "three/examples/jsm/controls/orbitControls.js";
// 导入GUI
  import { GUI } from 'three/examples/jsm/libs/lil-gui.module.min.js';

// 创建场景
const scene = new THREE.Scene();
// 创建相机
const camera = new THREE.PerspectiveCamera(
    45, //视角
    window.innerWidth / window.innerHeight, //宽高比
    0.1, //近平面
    1000,//原平面
);

//创建渲染器
const renderer = new THREE.WebGLRenderer();
//要渲染的宽高尺寸
renderer.setSize(window.innerWidth, window.innerHeight);
//将画布 挂载到dom中
document.body.appendChild(renderer.domElement);


// 创建一个几何体
const geometry = new THREE.BoxGeometry(1,1,1);
//创建材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });

//创建网格
const cube = new THREE.Mesh(geometry, material);
cube.position.set(2,0,0)
// 放大3倍
// cube.scale.set(2,2,2);


// 旋转45度
cube.rotation.x = Math.PI / 4;

scene.add(cube);

//将网格添加到场景中

//设置相机的位置
camera.position.z = 5;   //  x y z轴的距离  默认是0
camera.position.y = 3;
camera.position.x = 3;
camera.lookAt(3,0,0); // 默认看向原点

// 添加世界坐标辅助器
const axesHelper = new THREE.AxesHelper(5);
scene.add(axesHelper);

//添加轨道控制器
const controls = new OrbitControls( camera, renderer.domElement );

// renderer.render(scene, camera);
function animate() {
    controls.update();// 更新轨道控制器
  requestAnimationFrame(animate);// 关键帧调用  循环调用
  // cube.rotation.x += 0.01;
  // cube.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();

// 设置响应画布
window.addEventListener('resize', () => {
  //更新摄像头的宽高比
  camera.aspect = window.innerWidth / window.innerHeight;
  //更新摄像机的投影矩阵
  camera.updateProjectionMatrix();
  //更新渲染器
  renderer.setSize(window.innerWidth, window.innerHeight);
  //更新渲染器的像素比
  renderer.setPixelRatio(window.devicePixelRatio);
});



// 创建GUI 
const gui = new GUI();
//  添加按钮
let eventObj = {
  Fullscreen: function(){
    //全屏
    document.body.requestFullscreen();
  },
  ExitFullscreen: function(){
      //退出全屏
      document.exitFullscreen();
  }
}

gui.add(eventObj, 'Fullscreen').name('全屏')
gui.add(eventObj, 'ExitFullscreen').name('退出全屏')
//控制立方体的位置
// gui.add(cube.position,'x',-5,5).name('立方体的x轴位置');
gui.add(cube.position, 'x').min(0).max(10).step(0.01).name('立方体的x轴');
gui.add(cube.position, 'y').min(0).max(10).step(0.01).name('立方体的y轴');
gui.add(cube.position, 'z').min(0).max(10).step(0.01).name('立方体的z轴');

</script>
  
文件夹形式
let folder = gui.addFolder('立方体的位置'); 《-----关键点//
folder.add(cube.position, 'x').min(0).max(10).step(0.01).name('立方体的x轴');
folder.add(cube.position, 'y').min(0).max(10).step(0.01).name('立方体的y轴');
folder.add(cube.position, 'z').min(0).max(10).step(0.01).name('立方体的z轴').onChange((val)=>{
  console.log('立方体的z轴变化了',val);
});

folder.add(cube.position, 'y').min(0).max(10).step(0.01).name('立方体的y轴').onFinishChange((val)=>{
  console.log('立方体的y轴变化了',val);
});
```



开启线框模式

```
// 创建一个几何体
const geometry = new THREE.BoxGeometry(1,1,1);
//创建材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
//设置元素材质为线框模式
material.wireframe = true;


调式写法：
// material.wireframe = true;
folder.add(material, 'wireframe').name('线框模式切换');


// 自定义
let colorParams = {
  color: '#00ff00'
}
folder.addColor(colorParams, 'color').name('立方体材质的颜色').onChange((val)=>{
  cube.material.color.set(val);
});
```



![](.\img\2.png)



BufferGeometry 核心方法







### 三维空间里的角度描述

欧拉角是描述三维空间中物体旋转的三种角度表示方法。它由三个旋转角度组成，通常称为：

- **绕 X 轴的旋转角（Roll）**
- **绕 Y 轴的旋转角（Pitch）**
- **绕 Z 轴的旋转角（Yaw）**

在 [Three.js](https://zhida.zhihu.com/search?content_id=720509245&content_type=Answer&match_order=1&q=Three.js&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NDQ0Mjc3ODMsInEiOiJUaHJlZS5qcyIsInpoaWRhX3NvdXJjZSI6ImVudGl0eSIsImNvbnRlbnRfaWQiOjcyMDUwOTI0NSwiY29udGVudF90eXBlIjoiQW5zd2VyIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.xAvuyIkDY9BGTui614u-y1xylxhbRuhV_vnihcIZ5Jw&zhida_source=entity) 中，欧拉角通过 `THREE.Euler` 对象来实现。通过设置欧拉角的三个值，你可以控制物体在三维空间中的旋转。

案例：机器狗路线中的点， 需要以下 参数  x ,y ,z, Yaw角度。 地图上连续点击一组点，然后每个点内需要添加Yaw. 该数值的计算方法如下：

```js
import * as THREE from 'three';

// 定义三个点
const point1 = new THREE.Vector3(1, 0, 0);
const point2 = new THREE.Vector3(2, 0, 1);
const point3 = new THREE.Vector3(3, 0, 2);

// 计算每个点的 Yaw 角
function calculateYaw(pointA, pointB) {
    const direction = new THREE.Vector3().subVectors(pointB, pointA);
    // 归一化方向向量
    direction.normalize();
    // 计算 Yaw 角
    return Math.atan2(direction.z, direction.x);
}

// 计算从 point1 到 point2 的 Yaw 角
const yaw1 = calculateYaw(point1, point2);
// 计算从 point2 到 point3 的 Yaw 角
const yaw2 = calculateYaw(point2, point3);

console.log('Yaw from point1 to point2:', yaw1);
console.log('Yaw from point2 to point3:', yaw2);    
```

### 代码解释：

1. **导入 Three.js**：借助 `import` 语句导入 Three.js 库。
2. **定义点**：运用 `THREE.Vector3` 定义三个点。
3. **计算 Yaw 角**：`calculateYaw` 函数接收两个点作为参数，先算出这两个点之间的方向向量，再对该向量进行归一化处理，最后使用 `Math.atan2` 函数算出 Yaw 角。
4. **输出结果**：调用 `calculateYaw` 函数算出每个点的 Yaw 角，并将结果打印到控制台。



这样你就能算出三个点各自的 Yaw 角了。





