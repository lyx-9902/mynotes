# 项目常用css

## transition animation区别

**CSS中的`transition`和`animation`属性主要用于创建动态效果，‌但它们在实现方式、‌应用场景、‌性能以及与事件的交互方面存在显著区别。‌**

- **实现方式**：‌

  - `transition`是一个过渡属性，‌适用于简单的CSS属性变化过渡，‌需要触发事件（‌如鼠标移动或点击）‌才会执行动画。‌它类似于flash的补间动画，‌设置一个开始关键帧和一个结束关键帧，‌通过在CSS属性的变化过程中进行过渡，‌从而产生动态效果。‌
  - `animation`是一个动画属性，‌适用于创建更复杂和多样化的动画效果。‌它不需要触发事件，‌通过关键帧（‌@keyframes）‌定义动画效果。‌`animation`可以设置多个关键帧（‌用@keyframes定义）‌完成动画，‌类似于flash的补间动画，‌但提供了更大的灵活性和控制力。‌

  ### 案例

  ### transition 

  案例：对div width属性   100px  ->200px 的切换 添加过渡效果

```
  transition: 0.2s linear;
```

###  animation动画的使用：

特点： 关闭和打开的两种状态 都有关键帧样式代码。 一下效果是：大屏页面的leftPage的移动。

```
    @keyframes pageROpen {
        from {
            right: -480px;
        }

        to {
            right: 20px;
        }
    }

    @keyframes pageRClose {
        from {
            right: 20px;
        }

        to {
            right: -480px;
        }
    }

    .pageropen {
        animation: pageROpen 0.5s forwards;
    }

    .pagerclose {
        animation: pageRClose 0.5s forwards;
    }
```

