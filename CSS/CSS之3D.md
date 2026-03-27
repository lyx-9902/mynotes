3D图示

![](.\img\3d_axes.png)

3D transform中有下面这三个方法

- `rotateX( angle )`
- `rotateY( angle )`
- `rotateZ( angle )`

`rotate`旋转的意思，`rotateX`旋转X轴，`rotateY`旋转Y轴，`rotateZ`旋转Z轴…



### 必不可少的perspective属性

n.（观察问题的）视角，观点；透视（画）法；

`perspective`属性的存在与否决定了你所看到的是2次元的还是3次元的

### perspective属性的两种书写

`perspective`属性有两种书写形式，一种用在舞台元素上（动画元素们的共同父辈元素）；第二种就是用在当前动画元素上，与transform的其他属性写在一起。如下代码示例：

```css
.stage {
    perspective: 600px;
}
```

以及：

```css
#stage .box {
    transform: perspective(600px) rotateY(45deg);
}
```

### 理解perspective-origin

`perspective-origin`这个属性超级好理解，表示你那眼睛看的位置

```
perspective-origin: 25% 75%;
```



### transform-style: preserve-3d

`transform-style`属性也是3D效果中经常使用的，其两个参数，`flat|preserve-3d`. 前者`flat`为默认值，表示平面的；后者`preserve-3d`表示3D透视。



### backface-visibility

在CSS3的3D世界中，默认情况下，我们是可以看到背后的元素！因此，为了切合实际，我们常常会这样设置，使后面元素不可见：

```
backface-visibility:hidden;
```

