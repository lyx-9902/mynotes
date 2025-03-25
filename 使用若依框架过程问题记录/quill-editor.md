# vue-quill-editor踩坑记录--富文本内容回显样式不对

https://blog.csdn.net/weixin_43794749/article/details/123402192





使用vue-quill-editor写的富文本，内容在H5使用v-html显示时，样式跟在富文本写的时候样式不一样，字体大小显示不出来。
原因：有些类名，在v-html页面是没有找到的。
解决:
全局或者局部引入vue-quill-editor的样式文件
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'
1
2
3
<div v-html="content" class="ql-editor"></div>
1
一定要加上class="ql-editor"该类名，否则样式也不起作用
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/weixin_43794749/article/details/123402192