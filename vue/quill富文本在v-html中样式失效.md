# quill富文本在v-html中样式失效

https://blog.csdn.net/WCBandCTZ/article/details/139347636

富文本中的dom样式不起作用。关键点： 给v-html加上富文本的父级class

```
<div class="ql-container ql-snow">
            <div class="content msg-content ql-editor" v-html="newsList.newsDetails">
            </div>
        </div>
```

