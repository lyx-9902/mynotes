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





2026.06.10 

屏幕截图复制粘贴进编辑器中，图片编程base64格式，导致列表渲染图片时，接口携带数据较大，而卡滞。

解决方法是，pc上，拦截 粘贴行为，获取粘贴板的数据，上传oss，换回url，放到光标处。



以下是vue3 setup写法，注意格式。

```vue
<template>
  <div>
    <el-upload
      v-if="type === 'url'"
      :action="upload.url"
      :before-upload="handleBeforeUpload"
      :on-success="handleUploadSuccess"
      :on-error="handleUploadError"
      class="editor-img-uploader"
      name="file"
      :show-file-list="false"
      :headers="upload.headers"
    >
      <i ref="uploadRef"></i>
    </el-upload>
  </div>
  <div class="editor" ref="editorContainer">
    <quill-editor
      ref="quillEditorRef"
      v-model:content="content"
      content-type="html"
      :options="options"
      :style="styles"
      @text-change="(e: any) => $emit('update:modelValue', content)"
    />
  </div>
</template>

<script setup lang="ts">
import '@vueup/vue-quill/dist/vue-quill.snow.css';

import { QuillEditor, Quill } from '@vueup/vue-quill';
import { propTypes } from '@/utils/propTypes';
import { globalHeaders } from '@/utils/request';
// 重点：手动导入 Link 模块

import Link from 'quill/formats/link'  // 或 quill/modules/link（根据版本）

Quill.register('formats/link', Link) // 注册模块
defineEmits(['update:modelValue']);

const props = defineProps({
  /* 编辑器的内容 */
  modelValue: propTypes.string,
  /* 高度 */
  height: propTypes.number.def(400),
  /* 最小高度 */
  minHeight: propTypes.number.def(400),
  /* 只读 */
  readOnly: propTypes.bool.def(false),
  /* 上传文件大小限制(MB) */
  fileSize: propTypes.number.def(5),
  /* 类型（base64格式、url格式） */
  type: propTypes.string.def('url')
});

const { proxy } = getCurrentInstance() as ComponentInternalInstance;

const upload = reactive<UploadOption>({
  headers: globalHeaders(),
  url: import.meta.env.VITE_APP_BASE_API + '/resource/oss/upload'
});
const quillEditorRef = ref();
const uploadRef = ref<HTMLDivElement>();

const options = ref<any>({
  theme: 'snow',
  bounds: document.body,
  debug: 'warn',
  modules: {
    // 工具栏配置
    toolbar: {
      container: [
        ['bold', 'italic', 'underline', 'strike'], // 加粗 斜体 下划线 删除线
        ['blockquote', 'code-block'], // 引用  代码块
        [{ list: 'ordered' }, { list: 'bullet' }], // 有序、无序列表
        [{ indent: '-1' }, { indent: '+1' }], // 缩进
        [{ size: ['small', false, 'large', 'huge'] }], // 字体大小
        [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
        [{ color: [] }, { background: [] }], // 字体颜色、字体背景颜色
        [{ align: [] }], // 对齐方式
        ['clean'], // 清除文本格式
        ['link', 'image', 'video'] // 链接、图片、视频
      ],
      handlers: {
        image: (value: boolean) => {
          if (value) {
            // 调用element图片上传
            uploadRef.value.click();
          } else {
            Quill.format('image', true);
          }
        }
      }
    }
  },
  placeholder: '请输入内容',
  readOnly: props.readOnly
});

const styles = computed(() => {
  let style: any = {};
  if (props.minHeight) {
    style.minHeight = `${props.minHeight}px`;
  }
  if (props.height) {
    style.height = `${props.height}px`;
  }
  return style;
});

const content = ref('');
watch(
  () => props.modelValue,
  (v: string) => {
    if (v !== content.value) {
      content.value = v || '<p></p>';
    }
  },
  { immediate: true }
);

// 图片上传成功返回图片地址
const handleUploadSuccess = (res: any) => {
  // 如果上传成功
  if (res.code === 200) {
    // 获取富文本实例
    let quill = toRaw(quillEditorRef.value).getQuill();
    // 获取光标位置
    let length = quill.selection.savedRange.index;
    // 插入图片，res为服务器返回的图片链接地址
    quill.insertEmbed(length, 'image', res.data.url);
    // 调整光标到最后
    quill.setSelection(length + 1);
    proxy?.$modal.closeLoading();
  } else {
    proxy?.$modal.msgError('图片插入失败');
    proxy?.$modal.closeLoading();
  }
};

// 图片上传前拦截
const handleBeforeUpload = (file: any) => {
  const type = ['image/jpeg', 'image/jpg', 'image/png', 'image/svg'];
  const isJPG = type.includes(file.type);
  //检验文件格式
  if (!isJPG) {
    proxy?.$modal.msgError(`图片格式错误!`);
    return false;
  }
  // 校检文件大小
  if (props.fileSize) {
    const isLt = file.size / 1024 / 1024 < props.fileSize;
    if (!isLt) {
      proxy?.$modal.msgError(`上传文件大小不能超过 ${props.fileSize} MB!`);
      return false;
    }
  }
  proxy?.$modal.loading('正在上传文件，请稍候...');
  return true;
};

// 图片失败拦截
const handleUploadError = (err: any) => {
  proxy?.$modal.msgError('上传文件失败');
};

// --------------------------拦截粘贴事件 ---------------------------------------------
import axios from 'axios';
const quillInstance = ref<Quill | null>(null);
// 声明一个 ref 父节点引用
const editorContainer = ref<HTMLDivElement | null>(null); 

  // 监听粘贴事件
const handlePaste = (e: ClipboardEvent) => {
  console.log(666);
  const clipboardData = e.clipboardData || (window as any).clipboardData;
  if (!clipboardData) return;

  const items = clipboardData.items;
  if (!items) return;

  for (let i = 0; i < items.length; i++) {
    const item = items[i];

    if (item.kind === 'file' && item.type.startsWith('image/')) {
      const file = item.getAsFile();
      if (file) {
        e.preventDefault();
        uploadImage(file);
      }
    }

    if (item.type === 'text/html') {
      item.getAsString((html: string) => {
        const match = html.match(/<img[^>]+src=["']data:image\/(png|jpeg|jpg);base64,([^"']+)["']/);
        if (match) {
          const mimeType = `image/${match[1]}`;
          const base64Data = match[2];
          const file = base64ToFile(base64Data, `pasted.${match[1]}`, mimeType);
          e.preventDefault();
          uploadImage(file);
        }
      });
    }
  }
};
// 上传图片到服务器
const uploadImage = async (file: File) => {
  const formData = new FormData();
  formData.append('file', file);

  try {
    const res = await axios.post(upload.url, formData, {
      headers: {
        'Content-Type': 'multipart/form-data',
        ...upload.headers
      }
    });

    console.log('Paste upload response:', res.data);

    if (!quillInstance.value) {
      console.error('Quill instance is null');
      ElMessage.error('编辑器实例未初始化');
      return;
    }

    if (res.data.code === 200) {
      if (res.data.data && res.data.data.url) {
        const length = quillInstance.value.getSelection()?.index || quillInstance.value.getLength();
        quillInstance.value.insertEmbed(length, 'image', res.data.data.url);
        quillInstance.value.setSelection(length + 1);
      } else {
        console.error('Response data or URL is missing:', res.data);
        ElMessage.error('图片地址获取失败');
      }
    } else {
      ElMessage.error(res.data.msg || '图片上传失败');
    }
  } catch (error) {
    console.error('Upload error:', error);
    ElMessage.error('图片上传失败');
  }
};
// 工具方法
const base64ToFile = (base64Data: string, filename: string, mimeType: string): File => {
  const byteString = atob(base64Data);
  const arrayBuffer = new ArrayBuffer(byteString.length);
  const intArray = new Uint8Array(arrayBuffer);
  for (let i = 0; i < byteString.length; i++) {
    intArray[i] = byteString.charCodeAt(i);
  }
  return new File([intArray], filename, { type: mimeType });
};



onMounted(() => {
  console.log(quillEditorRef.value);
  console.log(toRaw(quillEditorRef.value).getQuill());
  quillInstance.value = toRaw(quillEditorRef.value).getQuill();
  editorContainer.value?.addEventListener('paste', handlePaste);
});

onUnmounted(() => {
  editorContainer.value?.removeEventListener('paste', handlePaste);
});
</script>

<style>
.editor-img-uploader {
  display: none;
}
.editor,
.ql-toolbar {
  white-space: pre-wrap !important;
  line-height: normal !important;
}
.quill-img {
  display: none;
}
.ql-snow .ql-tooltip[data-mode='link']::before {
  content: '请输入链接地址:';
}
.ql-snow .ql-tooltip.ql-editing a.ql-action::after {
  border-right: 0;
  content: '保存';
  padding-right: 0;
}
.ql-snow .ql-tooltip[data-mode='video']::before {
  content: '请输入视频地址:';
}
.ql-snow .ql-picker.ql-size .ql-picker-label::before,
.ql-snow .ql-picker.ql-size .ql-picker-item::before {
  content: '14px';
}
.ql-snow .ql-picker.ql-size .ql-picker-label[data-value='small']::before,
.ql-snow .ql-picker.ql-size .ql-picker-item[data-value='small']::before {
  content: '10px';
}
.ql-snow .ql-picker.ql-size .ql-picker-label[data-value='large']::before,
.ql-snow .ql-picker.ql-size .ql-picker-item[data-value='large']::before {
  content: '18px';
}
.ql-snow .ql-picker.ql-size .ql-picker-label[data-value='huge']::before,
.ql-snow .ql-picker.ql-size .ql-picker-item[data-value='huge']::before {
  content: '32px';
}
.ql-snow .ql-picker.ql-header .ql-picker-label::before,
.ql-snow .ql-picker.ql-header .ql-picker-item::before {
  content: '文本';
}
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value='1']::before,
.ql-snow .ql-picker.ql-header .ql-picker-item[data-value='1']::before {
  content: '标题1';
}
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value='2']::before,
.ql-snow .ql-picker.ql-header .ql-picker-item[data-value='2']::before {
  content: '标题2';
}
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value='3']::before,
.ql-snow .ql-picker.ql-header .ql-picker-item[data-value='3']::before {
  content: '标题3';
}
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value='4']::before,
.ql-snow .ql-picker.ql-header .ql-picker-item[data-value='4']::before {
  content: '标题4';
}
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value='5']::before,
.ql-snow .ql-picker.ql-header .ql-picker-item[data-value='5']::before {
  content: '标题5';
}
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value='6']::before,
.ql-snow .ql-picker.ql-header .ql-picker-item[data-value='6']::before {
  content: '标题6';
}
.ql-snow .ql-picker.ql-font .ql-picker-label::before,
.ql-snow .ql-picker.ql-font .ql-picker-item::before {
  content: '标准字体';
}
.ql-snow .ql-picker.ql-font .ql-picker-label[data-value='serif']::before,
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value='serif']::before {
  content: '衬线字体';
}
.ql-snow .ql-picker.ql-font .ql-picker-label[data-value='monospace']::before,
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value='monospace']::before {
  content: '等宽字体';
}
</style>

```

