# threeJS

## 网址

官网： https://threejs.org/

文档： https://threejs.org/manual/#zh/fundamentals

网络自建私网

www.three3d.cn

https://www.three3d.cn/docs/index.html#manual/zh/introduction/Creating-a-scene

学习指南：

https://www.three3d.cn/threejs/01-%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/01-%E5%89%8D%E7%AB%AF3D%E5%8F%AF%E8%A7%86%E5%8C%96Three.js%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF.html

bibi相关课程

https://www.bilibili.com/video/BV1Gg411X7FY?spm_id_from=333.788.videopod.episodes&vd_source=08704ab849ba956e9d7acbdbd55b0991&p=21

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

## tips提示

#### 00.三维空间里的角度描述

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

**计算Yaw角的思路：**

1. **导入 Three.js**：借助 `import` 语句导入 Three.js 库。
2. **定义点**：运用 `THREE.Vector3` 定义三个点。
3. **计算 Yaw 角**：`calculateYaw` 函数接收两个点作为参数，先算出这两个点之间的方向向量，再对该向量进行归一化处理，最后使用 `Math.atan2` 函数算出 Yaw 角。
4. **输出结果**：调用 `calculateYaw` 函数算出每个点的 Yaw 角，并将结果打印到控制台。



这样你就能算出三个点各自的 Yaw 角了。

#### 01.关于颜色值16进制问题

```
      //  创建地面依据模型包围盒的大小
        const geometry = new THREE.PlaneGeometry(size.x * 2, size.z * 2);
        const material = new THREE.MeshBasicMaterial({ color: 0x06c81c, side: THREE.DoubleSide });
        const ground = new THREE.Mesh(geometry, material);
        
        
   color: 0x06c81c,  
   
 插件获取的颜色值：#06c81c  这种格式的
```

在 JavaScript 里，`06c81c` 这种写法不符合规范，因为在 JavaScript 中，以 `0` 开头的数字会被当作八进制数，但八进制数里只能包含 `0 - 7` 的数字，而 `06c81c` 包含了 `c` ，这显然是错误的。

如果你想把 `06c81c` 当成十六进制数，正确的写法应该是 `0x06c81c` 。在 JavaScript 里，十六进制数要以 `0x` 开头。

#### 02 关于模型数据类型

  glb：已经转化位二进制

  gltf: json的文本格式    

  这两种，都可以使用gltfLoader加载器

#### 03 模型变黑的原因

如果加载了一个模型，全黑色，可能是模型设置的材质，需要全景光。

#### 04 帧率监测器工具

![](.\img\4.png)

数值越大越好，越流畅。

**性能评估**

- **直观展示性能指标**：Stats 可以实时显示帧率（FPS，Frames Per Second），也就是每秒显示的帧数。帧率是衡量图形应用程序性能的一个重要指标，它直观地反映了画面的流畅程度。例如，在一个游戏或 3D 可视化项目中，较高的帧率（如 60 FPS 或更高）通常意味着画面更加流畅，用户体验更好；而较低的帧率（如 20 FPS 或更低）会让画面出现卡顿，影响用户的使用感受。
- **评估硬件适配性**：通过观察帧率，开发者可以了解应用程序在不同硬件设备上的性能表现。如果在高端设备上帧率较低，可能是代码存在性能问题；而在低端设备上帧率不理想，可能需要考虑优化算法、减少模型复杂度或降低纹理分辨率等，以确保应用程序在不同硬件条件下都能有较好的性能表现。

**性能优化**

- **定位性能瓶颈**：在开发过程中，随着场景复杂度的增加，帧率可能会下降。Stats 可以帮助开发者实时监测帧率变化，当帧率出现明显下降时，开发者可以分析此时场景中发生的变化，例如是否添加了新的模型、材质或特效，从而定位性能瓶颈所在。例如，如果在添加了一个复杂的光照效果后帧率大幅下降，那么就可以针对这个光照效果进行优化。
- **验证优化效果**：在对代码进行优化后，开发者可以通过观察 Stats 显示的帧率来验证优化效果。如果优化后帧率明显提高，说明优化措施有效；如果帧率没有变化或甚至下降，那么就需要重新审视优化方案，寻找其他可能的优化点。

**调试和测试**

- **辅助调试**：在调试过程中，Stats 可以作为一个重要的参考工具。例如，当出现画面卡顿或异常时，查看帧率是否稳定可以帮助开发者判断问题是由于性能问题还是其他逻辑错误导致的。如果帧率正常但画面仍然有问题，那么可能是代码逻辑存在错误；如果帧率明显下降，那么就需要重点关注性能方面的问题。

- **测试不同场景**：在测试阶段，开发者可以使用 Stats 来测试不同场景下的性能表现。例如，在一个游戏中，测试不同关卡、不同场景下的帧率，确保在各种情况下应用程序都能保持稳定的性能。同时，还可以测试不同用户操作（如缩放、旋转、移动等）对帧率的影响，以便及时发现并解决潜在的性能问题。

  

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stats Example</title>
    <!-- 引入 Stats.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/stats.js/r17/Stats.min.js"></script>
    或者是
    import Stats from 'three/addons/libs/stats.module.js';  引入本地three方法
</head>

<body>
    <script>
        // 创建 Stats 实例
        const stats = new Stats();
        // 将 Stats 添加到页面中
        document.body.appendChild(stats.dom);

        function animate() {
            // 更新 Stats
            stats.update();

            // 这里可以添加你的动画逻辑

            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>

</html>

```

在这个示例中，我们引入了 Stats.js 库，并创建了一个 Stats 实例，将其添加到页面中。在 `animate` 函数中，我们调用 `stats.update()` 方法来更新帧率信息。这样，我们就可以实时看到页面的帧率情况。



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

#### 06. threejs中的几何体

##### a.从0搭建物体

   任何物体都是由小的三角形组成。称三角面片。一个正方形最少需要两个三角形，当然也可以无线增加面数，面数越多，模型越精细，同样，越消耗性能。

 数据属性BufferGeometry，其他胶囊体等形状都是由这个基础类构建。

如果创建一个正方形，想使用4个点来构建，那么需要添加索引属性，达到服用指定的点（三位数确定的三维中的位置）

```
   //  创建地面依据模型包围盒的大小
        const geometry = new THREE.PlaneGeometry(size.x * 2, size.z * 2);
          console.log(geometry) //打印这个几何体   attributes-》position-》此处

```



![](.\img\3.png)

一个几何体从创建，到添加到场景中。

​        几何体 + 材质 == add到创建的Mesh网格场景中   最终呈现出来物体。

```
// 1.创建一个几何体
const geometry = new THREE.BufferGeometry
// 创建顶点数据,顶点是有序的,每三个为一个顶点，逆时针为正面
const vertices = new Float32Array([
  //顶点1
  -1.0, -1.0, 1.0,
  //顶点2
  1.0, 1.0, 0,
  //顶点3
  1.0, -1.0, 0,
])
// 创建 顶点索引
geometry.setAttribute('position', new THREE.BufferAttribute(vertices, 3));
console.log(geometry);
// 2.创建材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 ,side: THREE.DoubleSide });



//3.创建网格
const cube = new THREE.Mesh(geometry, material);
cube.position.set(0,0,0)
scene.add(cube);
```

##### b. 提供的常见几何体搭建

 除了使用基础的三角面片构建外，threejs提供了常见的几何体的语法糖。例如： 立方体  

######  **立方体 BoxGeometry**

```js
代码示例
const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );
  构造器
BoxGeometry(width : Float, height : Float, depth : Float, widthSegments : Integer, heightSegments : Integer, depthSegments : Integer)
width — X轴上面的宽度，默认值为1。
height — Y轴上面的高度，默认值为1。
depth — Z轴上面的深度，默认值为1。
widthSegments — （可选）宽度的分段数，默认值是1。
heightSegments — （可选）高度的分段数，默认值是1。
depthSegments — （可选）深度的分段数，默认值是1。
```

###### 圆形缓冲几何体

（CircleGeometry）

###### 圆锥缓冲几何体

###### 圆柱缓冲几何体

###### 十二面缓冲几何体

###### 边缘几何体

###### 挤压缓冲几何体

###### 二十面缓冲几何体

###### 车削缓冲几何体

###### 八面缓冲几何体

###### 平面缓冲几何体

###### 多面缓冲几何体

###### 圆环缓冲几何体

###### 形状缓冲几何体

###### 球缓冲几何体

###### 四面缓冲几何体

###### 圆环缓冲几何体

###### 圆环缓冲扭结几何体

###### 管道缓冲几何体

###### 网格几何体

这个类可以被用作一个辅助物体，来对一个geometry以线框的形式进行查看。

#### 07 基础材质

基础材质 贴圏 高光 遙明 环境 光照 环境遮蔽贴图的用途  ，

可以配置全景图，对象模型的高光，反射，贴图，透明等材质特性。

```
//引入所有核心方法
import * as THREE from "three"
import { RGBELoader } from "three/examples/jsm/Addons.js";
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


// 创建纹理加载器
const textureLoader = new THREE.TextureLoader();
//加载纹理
const texture = textureLoader.load('/img/jinggai1.jpg');
//加载ao贴图  该纹理的红色通道用作环境遮挡贴图。
const aoTexture = textureLoader.load('/img/jinggai1.jpg');

//加载透明度贴图 alpha贴图是一张灰度纹理，用于控制整个表面的不透明度。（黑色：完全透明；白色：完全不透明）
const alphaTexture = textureLoader.load('/img/jinggai2.jpg');

//rgbeLoader 加载hdr贴图
let rgbeLoader = new RGBELoader();
rgbeLoader.load('/img/quanjingtu.hdr', ( envMap ) => {
  //设置球形贴图
    envMap.mapping = THREE.EquirectangularReflectionMapping;
     //设置环境贴图
    scene.background = envMap;
});

const geometry = new THREE.PlaneGeometry( 1, 1);
const material = new THREE.MeshBasicMaterial( {   <---- 配置的地方
  color: 0xffffff,
  map:texture,
  transparent:true,
  side: THREE.DoubleSide,
  aoMap:aoTexture,
  alphaMap:alphaTexture
} );

const cube = new THREE.Mesh( geometry, material );
```

######  纹理属性

如果加载模型，颜色过白，可能是颜色区间问题。 默认是linear线性颜色。 可以设置位sRGB

```
gui.add(texture, 'colorSpace',{
  sRGB: THREE.SRGBColorSpace,
  Linear: THREE.LinearSRGBColorSpace
}).onChange(()=>{
  material.needsUpdate = true;
}).name('颜色空间');
```



#### 08 雾 fog

 thresjs中，有一个类，专门生成雾气天气效果。  注意点：  线性雾和指数雾 。 默认线性雾。

```
// 创建长方体
const geometry = new THREE.BoxGeometry(1, 1, 80);
const material = new THREE.MeshBasicMaterial({
  color: 0x00ff00,
});
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );


// 创建场景fog
scene.fog = new THREE.Fog(0x999999, 0.1, 50); // 50m后看不清

// 创建场景指数雾
// scene.fog = new THREE.FogExp2(0x999999, 0.1);  //0.1值越小 雾越淡 看的稍远一些
scene.background = new THREE.Color(0x999999); //设置场景背景颜色和雾气的颜色一致

```

#### 09.加载模型

 场景中的物体由许多三角面片构成，但是实际开发中，例如一个城市场景，包含了太多的东西，一个一个的几何体添加肯定不行。所以一版由建模软件，构建一个想要的模型，加载到threejs的场景中。这里就要提到加载器

**GLTF加载器（GLTFLoader）**

用于载入*glTF 2.0*资源的加载器。

[glTF](https://www.khronos.org/gltf)（gl传输格式）是一种开放格式的规范 （[open format specification](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0)）， 用于更高效地传输、加载3D内容。该类文件以JSON（.gltf）格式或二进制（.glb）格式提供， 外部文件存储贴图（.jpg、.png）和额外的二进制数据（.bin）。一个glTF组件可传输一个或多个场景， 包括网格、材质、贴图、蒙皮、骨架、变形目标、动画、灯光以及摄像机。

**DracoLoader**

-个用于加载经过Draco压缩的图形库。
Draco是个开源的库，主要用于压缩和解压缩二维模型及点云。以客户端上解压缩为代价，显著减少压缩的图形。
 独立的Draco文件后缀为.drc，其中包含顶点坐标，法线，颜色和其他的属性，Draco文件*不*包含材质纹理，动画和节点结构-为了能使用这些特征，需要将Draco图形 嵌入到GLTF文件中。使用gITF-Pipeline可以将一个普通的GLTF文件转化为经过Draco压缩的GLTF文件。当使用Draco压缩的GLTF模型时，GLTFLoader内部会调用DRACOLoader.
      推荐创建一个DRACOLoader实例并重用，可以有效避免重复创建加载多个解压器实例

使用加载器的步骤

```
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js';  //引入加载器

 / 实例化加载器 gltf
  const dracoLoader = new DRACOLoader();    //1.实例化加载器
  dracoLoader.setDecoderPath('./draco/'); //2.设置解码器路径  

  // 加载 GLB 模型
  const loader = new GLTFLoader();
  loader.setDRACOLoader(dracoLoader); //告诉加载器使用 draco 解码器
  let model;
  loader.load('/models/gltf/robot4-min.glb', (gltf) => {
    model = gltf.scene;
    scene.add(model);
  });
  
  
  
  ********************************
    第2步的 /draco路径的文件。  
    threedemo\node_modules\three\examples\jsm\libs\draco  ==》拷贝到项目的public文件下
```

####  10 场景中的点击事件交互

​    三维场景中的点击规则，是通过相机的角度，相机位置点，到点击的屏幕位置，换算到三维场景中的坐标点，连成一条射线，来判断是否点击到了物体，或者说碰到了物体，如果多个物体排列在一条直线上，那么点击是可能同时点击到多个物体，一般默认射线穿过的第一个物体，为目标点击物。设计如下类：

**光线投射Raycaster**

这个类用于进行[raycasting](https://en.wikipedia.org/wiki/Ray_casting)（光线投射）。 光线投射用于进行鼠标拾取（在三维空间中计算出鼠标移过了什么物体）。

<img src=".\img\5.png" style="zoom:67%;" />

屏幕px坐标 转化鼠标向量的x,y值。 横向x ,纵轴y .

<img src=".\img\6.png" style="zoom:50%;" />



关键代码

```
// 创建场景
const scene = new THREE.Scene();
// 创建相机
const camera = new THREE.PerspectiveCamera(
    45, //视角
    window.innerWidth / window.innerHeight, //宽高比
    0.1, //近平面
    1000,//原平面
);

// 创建射线
const raycaster = new THREE.Raycaster();
//创建鼠标向量
const mouse = new THREE.Vector2();

window.addEventListener('click', (e) => {
  // 设置鼠标向量xy坐标
  e.preventDefault();  // 阻止默认表单提交行为
    const mouse = {
      x: (e.clientX/window.innerWidth) * 2 - 1,      屏幕坐标转换世界坐标
      y: -((e.clientY/window.innerHeight) * 2 - 1),
    };
    //通过摄像机和鼠标位置跟新射线
    raycaster.setFromCamera(mouse, camera);
    //计算物体和射线的焦点
    // const intersects = raycaster.intersectObjects(scene.children); // 监测所有物体，包含坐标轴。
    const intersects = raycaster.intersectObjects([cube,cube2]); // 也可以指定监测的物体
    console.log(intersects);// 返回一个数组，数组中包含所有相交的物体的点的相关信息

    // {
    //   distance: 相机相机与物体的距离
    //   face: 相交的物体的哪一面
    //   faceIndex: 相交的物体的哪一面的索引
    //   distanceToRay: 相机相机与物体的距离
    //   index: 相交的物体的索引
    //   instanceId: 相交的物体的实例id
    //   instanceMatrix: 相交的物体的实例矩阵
    //   instanceColor: 相交的物体的实例颜色
    //  object: 相交的物体    ---   例如点击后修改颜色 可以修改这里面的材质 中的颜色
    // }

   if (intersects.length > 0) {
    intersects[0].object._isSelect = true;
    intersects[0].object._originColor = intersects[0].object.material.color.getHex();
    intersects[0].object.material.color.set(0xff0000);
  }
});

```



#### 补间动画

补间(动画)(来自 in-between )是一个概念，允许你以平滑的方式更改对象的属性。你只需告诉它哪些属性要更改，当补间结束运行时它们应该具有哪些最终值，以及这需要多长时间，补间引擎将负责计算从起始点到结束点的值。









