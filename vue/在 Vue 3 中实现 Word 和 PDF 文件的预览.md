# 在 Vue 3 中实现 Word 和 PDF 文件的预览

1. Word 文件预览
对于 Word 文件预览，可以使用 vue-office 或者 docx-preview 这样的第三方库。这里以 docx-preview 为例：

安装依赖

```
npm install docx-preview@0.1.4 jszip
```

使用示例
在 Vue 组件中引入并使用 docx-preview：

```
<template>
  <div>
    <docx-preview :src="docxUrl" style="height: 100vh;" />
  </div>
</template>


<script setup>
import { ref } from 'vue';
import DocxPreview from 'docx-preview';

const docxUrl = ref('path/to/your/docx/file.docx');
</script>
```

项目案例：

```vue
<template>
    <div>
        <a-button @click="review">测试预览word</a-button>
        <div id="reportContainer" style="height: 100vh;"></div>
    </div>
</template>
<script setup>
import axios from 'axios'
import { ref } from 'vue';
import { ElLoading } from 'element-plus'
import { blobValidate } from '@/utils/ruoyi'
import { getToken } from '@/utils/auth'
import { renderAsync } from "docx-preview";
let downloadLoadingInstance;

function review(){
    var url = 'http://192.168.112.4:9000/yogkvirtualteach/2024/09/09/9efc9fea0ca64de88838a5a53fba3879.docx' 
    downloadLoadingInstance = ElLoading.service({ text: "正在下载数据，请稍候", background: "rgba(0, 0, 0, 0.7)", })
    let reportContainer = document.getElementById("reportContainer");
    axios({
      method: 'get',
      url: url,
      responseType: 'blob',
      headers: { 'Authorization': 'Bearer ' + getToken() }
    }).then((res) => {
      const isBlob = blobValidate(res.data);
      if (isBlob) {
        const blob = new Blob([res.data], { type: 'application/octet-stream' })
        renderAsync(blob,reportContainer,null)

      } else {
        this.printErrMsg(res.data,file.vaue);
      }
      downloadLoadingInstance.close();
    }).catch((r) => {
      console.error(r)
      Message.error('下载文件出现错误，请联系管理员！')
      downloadLoadingInstance.close();
    })
}
</script>
```



##  vue-office excel的预览

npm 安装插件



```vue
  <vue-office-excel  
      :src="filesurl"  //  直接使用附件地址（该地址放到浏览器中，会触发下载。不需要blob下载成二进制数据流）
       @rendered="renderedHandler" 
       @error="errorHandler" 
    />


<script setup>

    import VueOfficeExcel from '@vue-office/excel'
    //引入相关样式
    import '@vue-office/excel/lib/index.css'
```

