# 部署ollama大模型

硬件： win11本地机器

机带 RAM	16.0 GB (15.8 GB 可用)

显卡 12GB   NVIDIA GeForce RTX 3060

处理器	12th Gen Intel(R) Core(TM) i5-12400F   2.50 GHz

存储1.38 TB  已使用1.38 TB中的347GB



设备名称	DESKTOP-VH9PNCJ

设备 ID	245A4024-1DD5-4913-9BAF-D8ED37B616A7
产品 ID	00342-30692-44182-AAOEM
系统类型	64 位操作系统, 基于 x64 的处理器
笔和触控	为 10 触摸点提供触控支持



## ollama部署的硬件要求：

Ollama 部署的硬件核心就 3 个关键点，新手按这个标准选硬件，绝对不会踩坑：

1. **显卡显存是第一门槛**：决定能运行的模型大小，入门 4GB 显存（7B 模型），中端 8GB 显存（13B 模型），高端 24GB 显存（70B 模型）；
2. **内存兜底防卡死**：有独显时 16GB 起步，32GB 流畅；纯 CPU 运行时 32GB 起步，64GB 保底；
3. **磁盘选 SSD 即可**：容量预留 2 倍模型大小，NVMe SSD 加载模型更快，无其他特殊要求。



##  三、结合 Ollama 部署：这套机器能跑什么？

直接给你一个**可直接参考的结论**：

### ✅ 完全流畅、无压力

- 7B 模型（Llama3、Qwen2、Gemma 等）

  - q4_0 /q5_K_M 量化
  - 推理速度快，几乎秒回，内存 / 显存都很轻松。

  

### ✅ 流畅，体验良好

- 13B 模型（Llama3 13B、Qwen2 13B 等）

  - q4_0 /q5_K_M 量化
  - 12GB 显存刚好能吃下，速度不错，适合日常使用。

  

### ⚠️ 能跑，但需要注意资源

- 34B 模型（Llama3 34B、Qwen2 34B 等）

  - 只能跑 **q4_0 量化**
  - 显存基本占满，内存也会吃不少
  - 推理速度会变慢，适合尝鲜、不适合高频使用。

  

### ❌ 不推荐

- 70B 模型：显存不够，基本跑不起来或极慢。
- 纯 CPU 跑大模型：没必要，你有 3060 12GB，用 GPU 即可



### 如何判断那个模型可以运行在自己电脑上

要判断哪个 DeepSeek 模型可以在你的电脑上运行，你可以从这几个方面来快速筛选：

### 1. 查看模型的硬件需求

- 参数大小

  ：在每个模型标签里会标注，比如 

  ```
  1.5b
  ```

  ```
  7b
  ```

  ```
  671b
  ```

  - **小模型（如 1.5B、7B）**：对硬件要求较低，一般消费级显卡（如 RTX 3060/3070 等，8GB 以上显存）就能运行。
  - **大模型（如 67B、671B）**：需要专业级显卡（如 A100、RTX A6000 等，40GB 以上显存），普通个人电脑很难满足。

  

- **量化版本**：Ollama 上的模型通常会提供不同量化版本（如 Q4_K_M、Q8_0），量化程度越高（如 Q4），对显存的要求越低，越适合在普通电脑上运行。

### 2. 检查模型的支持标签

在你截图里的模型卡片上，有几个关键标签可以参考：

- **`cloud`**：这类模型主要为云环境设计，本地运行难度较大。
- **没有 `cloud` 标签**：比如 `deepseek-r1`（带 `1.5b`、`7b` 等标签）、`deepseek-ocr`，通常更适合本地部署。

### 3. 用 Ollama 命令行快速验证

1. 打开终端，输入 `ollama run <模型名>` 来尝试拉取并运行模型（如 `ollama run deepseek-r1:7b`）。
2. 如果你的硬件不够，Ollama 会给出提示，或者在启动时直接崩溃。
3. 你也可以先用 `ollama show <模型名>` 查看模型的详细硬件需求。

### 4. 按推荐优先级选择

- **最适合新手本地运行**：`deepseek-r1:7b` 或 `deepseek-r1:1.5b`，对显存要求低，性能也不错。
- **如果你的显卡很强（24GB 以上显存）**：可以尝试 `deepseek-r1:32b`。
- **避免尝试**：`deepseek-v3`、`deepseek-v3.1`、`deepseek-v3.2` 这类 671B 参数的模型，普通电脑几乎无法运行。

## 四、本机安装7B模型，重在记录部署方法

https://ollama.com/search?page=2&q=deepseek

```
deepseek-r1
DeepSeek-R1是一个开放推理模型系列，其性能接近主流模型，例如O3和Gemini 2.5 Pro。
tools  thinking 1.5b  7b 8b 14b 32b 70b  671b
```

​    查看ollama可以安装哪些模型， 查看models列表中，

​     1.查看模型的功能，是否为逻辑推理 的，对话的。

​     2. 查看参数量， 7b以下一般4g + 12GB显卡 ，一般的电脑可以运行。

```
 安装模型：下载指令  ollama run 模型名字：参数量
ollama run deepseek-r1:7b
```

### 下载 / 运行注意点

1. 模型文件默认保存在`C:\Users\你的用户名\.ollama\models`，无需修改路径；
2. 下载过程中不要关闭 cmd，断网会重新下载，耐心等待即可；
3. 若下载速度慢，无需手动干预，Ollama 支持断点续传，断网后重新输入命令会继续下载。



## 第四步：7B 模型基本使用（对话 / 退出 / 重启）

### 1. 正常对话

进入`>>> `提示符后，直接输入文字提问，回车即可得到回答，比如：

plaintext

```
>>> 你好，用Python写一个快速排序代码
>>> 解释一下人工智能的核心概念
>>> 总结一下今天的天气（可结合实际问题）
```

- 支持多轮对话，模型会记住上下文；

### 2. 退出对话界面

在`>>> `提示符下，输入以下任意一个命令，回车即可退出，后台服务不会关闭：

bash  运行

```
/exit
# 或
/quit
```

### 3. 重新启动模型

退出后，若想再次和 7B 模型聊天，无需重新下载，直接在 cmd 中输入原模型命令即可，秒启动：

bash  运行

```
ollama run llama3:7b  # 重启Llama3 7B
# 或
ollama run qwen2:7b   # 重启Qwen2 7B
```

## 五、第五步：常用辅助操作（模型管理 / 后台服务）

### 1. 查看本地已安装的模型

想知道自己装了哪些模型，输入以下命令：

bash  运行

```
ollama list
```

会显示模型名称、标签、大小，比如：

plaintext

```
llama3:7b   	sha256:xxxxxx   	3.8 GB   	ollama v0.1.48
```

### 2. 删除无用模型（释放磁盘空间）

如果装了多个模型，想删除其中一个，输入以下命令（替换为你的模型名）：

bash  运行

```
ollama rm llama3:7b
```

### 3. 重启 Ollama 后台服务（偶尔卡顿 / 显卡识别异常时用）

如果模型运行卡顿，或显卡加速突然失效，按下`Win+R`输入`services.msc`，打开**服务**窗口，找到**Ollama Service**，右键**重启**即可，再重新运行模型。

## 六、避坑小技巧（Win11 专属，新手必看）

1. **不要用管理员身份运行 cmd**：普通用户的 cmd 即可，管理员身份可能导致显卡驱动识别异常；
2. **关闭杀毒软件 / 防火墙**：部分杀毒软件会拦截 Ollama 的网络下载和后台服务，下载模型时临时关闭，完成后再打开；
3. **后台不要开高内存程序**：运行模型时，关闭虚拟机、大型游戏、多个浏览器标签，避免 16GB 内存被占满导致卡顿；
4. **模型下载失败**：重新输入`ollama run 模型名`，Ollama 支持断点续传，无需重新下载全部文件。

## 七、你的配置运行效果预期

你的 RTX3060 12G+16GB 内存运行 7B q4_0 量化模型，**推理速度极快**：

- 单轮提问响应时间**1-2 秒**，几乎秒回；
- 多轮对话无卡顿，显存占用仅 3-4GB，剩余 8GB 左右显存，内存占用约 6-8GB，系统剩余内存足够；
- 完全支持离线运行：模型下载完成后，断网也能正常聊天，无需网络。

### 总结

你的 Win11 机器装 7B 模型的核心步骤就 4 个：**装 Ollama→验证显卡加速→cmd 拉取模型→直接对话**，全程 10 分钟内搞定，所有命令直接复制即可，无需复杂配置。







## 使用模型的几种方法

### 第一种： 

```
ollama run llama3:7b  本机安装的模型
```

在命令行中，执行指令跑起来后，可以在shell命令行中，直接对话。

### 第二种： js API调用方法。

 本机win11 下载安装包，安装成功后，自动创建api接口访问服务。通过下面测试 是否返回模型列表，判断是否正常。

```
http://localhost:11434/api/tags
```

 如下返回，则成功。

```json
{
models: [
{
name: "llama3:latest",
model: "llama3:latest",
modified_at: "2026-02-04T09:31:01.9504166+08:00",
size: 4661224676,
digest: "365c0bd3c000a25d28ddbf732fe1c6add414de7275464c4e4d1c3b5fcb5d8ad1",
details: {
parent_model: "",
format: "gguf",
family: "llama",
families: [
"llama"
],
parameter_size: "8.0B",
quantization_level: "Q4_0"
}
},
{
name: "gemma3:1b",
model: "gemma3:1b",
modified_at: "2026-02-04T09:19:19.3241767+08:00",
size: 815319791,
digest: "8648f39daa8fbf5b18c7b4e6a8fb4990c692751d49917417b8842ca5758e7ffc",
details: {
parent_model: "",
format: "gguf",
family: "gemma3",
families: [
"gemma3"
],
parameter_size: "999.89M",
quantization_level: "Q4_K_M"
}
}
]
}
```



js调用代码，

```javascript
// 单轮对话
async function generateResponse() {
  const prompt = "解释一下什么是大语言模型";
  const model = "llama3:7b";

  try {
    const response = await fetch("http://localhost:11434/api/generate", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        model: model,
        prompt: prompt,
        stream: false, // 关闭流式输出，直接获取完整结果
      }),
    });

    const data = await response.json();
    console.log("模型回答：", data.response);
    // 把结果展示到页面上
    document.getElementById("result").textContent = data.response;
  } catch (error) {
    console.error("调用出错：", error);
  }
}

// 调用函数
generateResponse();
```



注意点： 本地测试案例为vue3项目，访问本地ollama项目，关于跨域分为两部分:一个是vite.config.js需要配置跨域，第二个需要ollama配置跨域。

> **注意**：浏览器会有跨域限制（CORS），如果遇到 `Access-Control-Allow-Origin` 错误，需要在启动 Ollama 时加上跨域参数：bash运行
>
> ```
> OLLAMA_ORIGINS="*" ollama serve
> ```

## 四、常用 API 接口速查

|       接口用途       |      地址       | 请求方法 |
| :------------------: | :-------------: | :------: |
|     生成单轮回答     | `/api/generate` |   POST   |
| 多轮对话（带上下文） |   `/api/chat`   |   POST   |
|     列出本地模型     |   `/api/tags`   |   GET    |
|      拉取新模型      |   `/api/pull`   |   POST   |
|       删除模型       |  `/api/delete`  |  DELETE  |

   本项目：使用了多轮对话  列出本地模型 两个接口。





## 项目使用案例：

```
<template>
  <div class="ollama-chat-container">
    <!-- <h1 class="title">ollama+Llama3对话界面</h1> -->
    <!-- 对话列表 -->
    <div class="chat-list" ref="chatListRef">
      <div 
        v-for="(msg, index) in chatMessages" 
        :key="index" 
        :class="['chat-item', msg.role]"
      >
        <div class="avatar">{{ msg.role === 'user' ? '我' : 'DeepSeek' }}</div>
        <!-- 改为v-html渲染Markdown解析后的HTML，移除原{{}}插值 -->
        <div class="content" v-html="msg.content"></div>
      </div>
    </div>

    <!-- 输入区域 -->
    <div class="input-area">
      <textarea
        v-model="inputMessage"
        placeholder="请输入你想提问的问题（比如：写一个Vue3组件）"
        class="input-text"
        @keyup.enter.prevent="handleSend" 
        @keydown.shift.enter="handleShiftEnter" 
      ></textarea>
      <button 
        @click="handleSend" 
        :disabled="loading || !inputMessage.trim()"
        class="send-btn"
      >
        {{ loading ? '思考中...' : '发送' }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue'
import axios from 'axios'
// 引入Markdown解析和代码高亮相关
import { marked } from 'marked'
import hljs from 'highlight.js'
// 引入代码高亮样式（可替换为其他样式，参考hljs官网）
import 'highlight.js/styles/github-dark.css'
// 引入代码复制插件
// 其他import不变
// import { useClipboard } from 'vue-clipboard3'
import useClipboard from 'vue-clipboard3'
// import 'vue3-copy-code/dist/style.css'
// 初始化剪贴板
const { toClipboard } = useClipboard()
// 注册代码复制指令（Vue3全局指令注册）
// const app = ref()
// copyCodePlugin(app)
// 复制代码的方法
const copyCode = async (code) => {
  try {
    await toClipboard(code)
    alert('代码已复制到剪贴板！')
  } catch (error) {
    alert('复制失败，请手动复制！')
  }
}
// 对话消息列表（初始消息改为Markdown渲染）
const chatMessages = ref(
  [{ role: 'assistant', content: marked.parse('你好！有什么可以帮你的？') }]
)
// 输入框内容
const inputMessage = ref('')
// 加载状态
const loading = ref(false)
// 对话列表Ref，用于自动滚动到底部
const chatListRef = ref(null)

// 配置marked，结合highlight.js实现代码高亮
marked.setOptions({
  highlight: (code, lang) => {
    // 有指定语言且hljs支持则高亮，否则自动识别
    if (lang && hljs.getLanguage(lang)) {
      return hljs.highlight(code, { language: lang }).value
    }
    return hljs.highlightAuto(code).value
  },
  gfm: true, // 开启GitHub风格Markdown（表格、代码块等）
  breaks: true, // 换行符转为<br>
  headerIds: false, // 关闭标题自动生成ID
  mangle: false // 关闭链接标签混淆
})

// Shift+Enter实现换行功能
const handleShiftEnter = (e) => {
  e.preventDefault()
  const textarea = e.target
  const start = textarea.selectionStart
  const end = textarea.selectionEnd
  // 在光标位置插入换行符
  inputMessage.value = 
    inputMessage.value.substring(0, start) + 
    '\n' + 
    inputMessage.value.substring(end)
  // 重置光标位置到换行后
  nextTick(() => {
    textarea.selectionStart = textarea.selectionEnd = start + 1
  })
}

// 自动滚动到底部
const scrollToBottom = () => {
  nextTick(() => {
    if (chatListRef.value) {
      chatListRef.value.scrollTop = chatListRef.value.scrollHeight
    }
  })
}

// 流式调用（保留你的system提示，优化Markdown渲染）
const callOllamaStream = async (message) => {
  try {
    // 解析用户输入的Markdown并添加到列表
    const userMdContent = marked.parse(message)
    chatMessages.value.push({ role: 'user', content: userMdContent })
    scrollToBottom()

    // 初始化助手消息（空内容，用于拼接流式响应）
    const assistantMsgIndex = chatMessages.value.length - 1
    chatMessages.value.push({ role: 'assistant', content: '' })

    // 调用Ollama真实本地接口（默认11434端口，api/chat为流式接口）
    const response = await fetch('http://192.168.0.251:5173/ollama/api/chat', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'llama3:latest', // 你的模型名，可根据实际拉取的修改
        messages: [
          { 
            role: 'system', 
            content: '你是一个基于Llama3模型的智能助手，回答简洁自然，不要包含任何标签或英文草稿。' 
          },
          // 传递纯文本给模型（避免Markdown标签干扰）
          ...chatMessages.value.slice(0, assistantMsgIndex + 1).map(msg => ({ 
            role: msg.role, 
            content: msg.role === 'user' ? message : marked.parse(msg.content) // 还原纯文本
          }))
        ],
        stream: true, // 开启流式响应
        temperature: 0.7,
        max_tokens: 4096 // 最大生成token数，可根据需求调整
      })
    })

    // 处理流式数据
    const reader = response.body.getReader()
    const decoder = new TextDecoder('utf-8')
    let assistantContent = '' // 拼接助手纯文本内容

    while (true) {
      const { done, value } = await reader.read()
      if (done) break

      // 解析Ollama流式响应（逐行JSON，过滤空行）
      const chunks = decoder.decode(value).split('\n').filter(Boolean)
      for (const chunk of chunks) {
        try {
          const data = JSON.parse(chunk)
          if (data.message?.content) {
            // 拼接纯文本内容
            assistantContent += data.message.content
            // 实时解析为Markdown并更新，实现打字机+Markdown渲染效果
            chatMessages.value[assistantMsgIndex + 1].content = marked.parse(assistantContent)
            scrollToBottom() // 每拼接一次滚动一次
          }
        } catch (e) {
          console.log('流式数据解析忽略：', e)
        }
      }
    }
  } catch (error) {
    console.error('流式调用失败：', error)
    chatMessages.value.push({ 
      role: 'assistant', 
      content: marked.parse('⚠️ **调用失败**：请检查Ollama是否启动、模型是否拉取成功！<br>1. 启动命令：`ollama serve`<br>2. 拉取模型：`ollama pull deepseek-r1:32b`')
    })
  } finally {
    loading.value = false
    scrollToBottom()
  }
}

// 发送消息处理
const handleSend = async () => {
  const message = inputMessage.value.trim()
  if (!message || loading.value) return

  loading.value = true
  inputMessage.value = '' // 清空输入框

  // 调用流式接口（保留你的选择，注释掉了非流式）
  await callOllamaStream(message)
  // await callOllamaNonStream(message) // 非流式调用（如需使用可解开注释）
}

// 非流式调用（同步修改为Markdown渲染，备用）
const callOllamaNonStream = async (message) => {
  try {
    const userMdContent = marked.parse(message)
    chatMessages.value.push({ role: 'user', content: userMdContent })
    scrollToBottom()

    const response = await axios.post('http://192.168.0.251:5173/ollama/api/chat', {
      model: 'llama3:latest',
      messages: [
        { 
          role: 'system', 
          content: '你是一个基于Llama3模型的智能助手，回答简洁自然，不要包含任何标签或英文草稿。' 
        },
        ...chatMessages.value.map(msg => ({ 
          role: msg.role, 
          content: marked.parse(msg.content) 
        }))
      ],
      stream: false,
      temperature: 0.7
    })
    // 解析AI响应为Markdown
    const aiMdContent = marked.parse(response.data.message.content)
    chatMessages.value.push({ role: 'assistant', content: aiMdContent })
  } catch (error) {
    console.error('非流式调用失败：', error)
    chatMessages.value.push({ 
      role: 'assistant', 
      content: marked.parse('⚠️ **调用失败**：请检查Ollama服务状态！')
    })
  } finally {
    loading.value = false
    scrollToBottom()
  }
}

// 页面挂载时检查Ollama服务是否可用
onMounted(async () => {
  scrollToBottom()
  try {
    // 调用Ollama的tags接口检查服务
    await axios.get('http://192.168.0.251:5173/ollama/api/tags').then(res => {
      console.log(res.data)
    })
    console.log('✅ Ollama服务已连接，DeepSeek模型可正常调用')
  } catch (error) {
    chatMessages.value.push({ 
      role: 'assistant', 
      content: marked.parse('⚠️ **未检测到Ollama服务**<br>1. 请先启动Ollama：`ollama serve`<br>2. 拉取DeepSeek32B模型：`ollama pull deepseek-r1:32b`<br>3. 确保模型名与代码中一致！')
    })
  }
})
</script>

<style scoped>

.ollama-chat-container {
  width: 1000px;
  margin: 20px auto;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  overflow: hidden;
}

.chat-list {
  height: 600px;
  padding: 20px;
  overflow-y: auto;
  background-color: #f9fafb;
  /* 优化滚动体验 */
  scroll-behavior: smooth;
}

.chat-item {
  display: flex;
  margin-bottom: 16px;
  gap: 12px;
  align-items: flex-start;
}

.chat-item.user {
  justify-content: flex-start;
  flex-direction: row-reverse; /* 用户名侧，头像在右 */
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #4f46e5;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  flex-shrink: 0;
}

.chat-item.user .avatar {
  background-color: #10b981;
}

.content {
  max-width: 70%;
  padding: 12px 16px;
  border-radius: 8px;
  font-size: 14px;
  line-height: 1.6;
  word-wrap: break-word;
}

.chat-item.user .content {
  background-color: #4f46e5;
  color: white;
}

.chat-item.assistant .content {
  background-color: white;
  border: 1px solid #e5e7eb;
}

.input-area {
  display: flex;
  gap: 12px;
  padding: 16px;
  border-top: 1px solid #e5e7eb;
  background-color: white;
  align-items: flex-end;
}

.input-text {
  flex: 1;
  padding: 12px;
  border: 1px solid #e5e7eb;
  border-radius: 4px;
  resize: none;
  height: 80px;
  font-size: 14px;
  outline: none;
}

/* 输入框聚焦样式 */
.input-text:focus {
  border-color: #4f46e5;
  box-shadow: 0 0 0 2px rgba(79, 70, 229, 0.1);
}

.send-btn {
  padding: 0 24px;
  height: 44px;
  background-color: #4f46e5;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.2s;
}

.send-btn:disabled {
  background-color: #94a3b8;
  cursor: not-allowed;
}

.send-btn:hover:not(:disabled) {
  background-color: #4338ca;
}

/* 关键：适配Markdown样式（scoped需用:deep穿透） */
:deep(.content h1) {
  font-size: 1.4rem;
  margin: 0.8rem 0 0.4rem;
  padding-bottom: 0.3rem;
  border-bottom: 1px solid #e5e7eb;
}

:deep(.content h2) {
  font-size: 1.2rem;
  margin: 0.7rem 0 0.3rem;
  padding-bottom: 0.2rem;
  border-bottom: 1px solid #e5e7eb;
}

:deep(.content h3) {
  font-size: 1.1rem;
  margin: 0.6rem 0 0.2rem;
}

:deep(.content p) {
  margin: 0.5rem 0;
}

:deep(.content ul, .content ol) {
  margin: 0.5rem 0 0.5rem 2rem;
  padding: 0;
}

:deep(.content li) {
  margin: 0.3rem 0;
}

/* 行内代码样式 */
:deep(.content code) {
  padding: 0.1rem 0.3rem;
  border-radius: 4px;
  font-family: 'Consolas', 'Monaco', monospace;
  font-size: 0.9rem;
  background-color: rgba(79, 70, 229, 0.1);
}

/* 代码块样式 */
:deep(.content pre) {
  background-color: #1f2937;
  color: #f9fafb;
  padding: 1rem;
  border-radius: 8px;
  overflow-x: auto;
  margin: 0.8rem 0;
  position: relative;
}

:deep(.content pre code) {
  background-color: transparent;
  padding: 0;
  color: inherit;
  font-size: 0.9rem;
  line-height: 1.5;
}

/* 引用样式 */
:deep(.content blockquote) {
  border-left: 4px solid #4f46e5;
  padding: 0.5rem 1rem;
  margin: 0.8rem 0;
  background-color: rgba(79, 70, 229, 0.05);
  color: #4b5563;
}

/* 链接样式 */
:deep(.content a) {
  color: #2563eb;
  text-decoration: underline;
}

/* 表格样式 */
:deep(.content table) {
  border-collapse: collapse;
  width: 100%;
  margin: 1rem 0;
}

:deep(.content th, .content td) {
  border: 1px solid #e5e7eb;
  padding: 0.6rem;
  text-align: left;
}

:deep(.content th) {
  background-color: #f3f4f6;
  font-weight: bold;
}

/* 代码复制按钮样式适配 */
:deep(.copy-code-wrapper) {
  position: relative;
}

:deep(.copy-code-btn) {
  position: absolute;
  top: 8px;
  right: 8px;
  background-color: #4f46e5;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 0.3rem 0.5rem;
  font-size: 0.8rem;
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.2s;
}

:deep(.copy-code-wrapper:hover .copy-code-btn) {
  opacity: 1;
}

/* 适配用户侧的Markdown白色文字 */
.chat-item.user :deep(.content code) {
  background-color: rgba(255, 255, 255, 0.2);
}

.chat-item.user :deep(.content blockquote) {
  background-color: rgba(255, 255, 255, 0.1);
  color: #e5e7eb;
  border-left-color: #a5b4fc;
}

.chat-item.user :deep(.content a) {
  color: #a5b4fc;
}
</style>
```











