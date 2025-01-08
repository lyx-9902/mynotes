# uni-app  开发App



[HBuilderX生成本地打包App资源](https://www.cnblogs.com/Jeely/p/11139715.html)



HBuilderX 打包 app有两种方式：

云打包 和本地打包

区别：





时长常见的消息推送

场景： 微信聊天， 手机消息提醒，app中内消息推送。

品牌：  个推 环信  友盟  网易云信  野火  极光 



## 唤起系统软键盘

```vue
<template>

  <view @click="click">评论{{ focus }}</view>

  <input placeholder="写评论" maxlength="200" :focus="focus" v-model="message" />

</view>

</template>

<script setup>
import { ref } from 'vue'

const message = ref("");
const focus = ref(false);

function click() {
	focus.value = !focus.value;  
}

</script>

```

