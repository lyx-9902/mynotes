通常我们用遮罩后会覆盖到一些需要点击的事件例如：

```
<div class="demo" click="aaa">111</div>
<div class="mask"></div>
<style>
   .mask{
              width:100%;
              height:100vh;
              background-color:rgba(0,0,0,.5);
              position: absolute;
              left: 0;
              top: 0;
          }
</style>
```



此时mask类名的元素就会遮挡住demo类名的元素，而且demo类名的aaa点击事件也就无法点击了。而[pointer-events](https://so.csdn.net/so/search?q=pointer-events&spm=1001.2101.3001.7020): none;就是让aaa这个点击事件可以继续能够点击到，还不影响mask的遮罩。

```
<div class="demo" click="aaa">111</div>
<div class="mask"></div>
<style>
   .mask{
              width:100%;
              height:100vh;
              background-color:rgba(0,0,0,.5);
              position: absolute;
              left: 0;
              top: 0;
              pointer-events: none;
          }
</style>
```

