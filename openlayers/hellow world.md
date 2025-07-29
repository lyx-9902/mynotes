

openlayers默认 坐标系 墨卡托（EPSG:3857），不是经纬度坐标系（EPSG:4326)。







![](.\img\1.png)



### 地图的构成

通过这个参数的名字我可以推断一个 map 可以设置多个 1ayer，[图层是构成openlayers的基本单位，地图是由多个layer组成的，这种设计类似于Photoshop里面的图层，多个图层是可以叠加的，在最上面的会覆盖下面的。

![](.\img\2.png)



###  核心概念



<img src=".\img\3.png" style="zoom:50%;" />



Openlayers的核心概念:

```
1、一张 Map 是由很多 Layer 图层组成的。
2、一个 Layer 对应一个 Source 矢量数据源
3、一个Source 由很多 Feature 组成
4、Feature是Geometry和 style 组成
```



```
  // 初始化地图
  map = new ol.Map({
    target: mapRef.value,
    layers: [gaodeLayer], // 加载高德图层
    view: new ol.View({
      center:[116.3972, 39.9075], // 初始中心点：北京
      zoom: 12, // 初始缩放级别（1-18）
      maxZoom: 18, // 最大缩放级别
      minZoom: 3 ,// 最小缩放级别
      projection: 'EPSG:4326'
    })
  });
```

**EPSG:4326** 是一个在 GIS(地理信息系统)中使用的坐标参考系(Coordinate Reference System)代码。它表示一个地理坐标系，即使用经纬度来表示地理位置。EPSG代码是由 European Petroleum Survey Group 分配的，它是一个用于统一管理坐标参考系的代码。4326代码是在 WGS 84(世界大地测量系统)椭球体模型的基础上定义的。EPSG:4326 常被用于在网络上传输地理位置信息，如在 Web 地图服务和地理位置 API 等。EPSG:4326 的经纬度范围是:经度范围在 -180°到 180°之间，纬度范围在 -90°到 90°之间。
总结通过以下代码解读，我可以得出一个结论，一个 ol的地图，主要由 1ayer 和 view 组成。layer可以有多个，view只能设置一个。

### EPSG:4326和 EPSG:3857的区别

**EPSG:4326** 和 **EPSG:3857** 是两个常用的坐标参考系代码，用于在 GIS 中表示地理位置。它们的主要区别如下:
**EPSG:4326** 表示一个地理坐标系，使用经纬度来表示地理位置，通常用于地理位置的显示和制图。
**EPSG:3857** 表示一个 Web 墨卡托坐标系，使用平面墨卡托投影来表示地理位置。

EPSG:3857 在在线地图中被广泛使用，因为它能够在 Web 地图上提供更高的精度和更好的分辨率。然





### 1、geojson定义

geojson 数据是矢量数据，是包含地理信息的json数据，格式是以key:value的形式存在的。后缀以 geojson结尾.

  geojson数据，可以自行编写，或者是通过相关网站工具创建。 例如阿里的datavhttps://datav.aliyun.com/portal/school/atlas/area_selector



### 第二章 Canvas

本章节讲解Canvas如何结合 0penlayer 使用，首先我们讲解Canvas的绘图基础。
我们初始化地图的时候可以看见，实际上Openlayer的地图就是用Canvas实现绘制的。

1、概念
什么是canvasHTML5<canvas>元素用于图形的绘制，区别于css，它的绘制通过 Javascript 来完成绘制。<canvas>标签只是 图形容器，您必须使用脚本来绘制图形Canvas API主要聚焦于2D图形。同时<canvas>元素的 WebGL API 则用于绘制硬件加速的2D和3D图形。







