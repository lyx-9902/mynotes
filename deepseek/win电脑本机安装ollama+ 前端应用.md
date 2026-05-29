# deepseek在前端落地应用

## 官网

ollama中文官网（网友翻译网站） https://ollama.cadn.net.cn

英文官网 **https://ollama.com**

```shell
curl http://localhost:11434/api/generate -d '{"model": "gemma3:1b","prompt": "Why is the sky blue?"}'
```

![](.\img\01.png)

## 安装

首先win 安装ollama的 exe软件的软件是比较方便的，安装后，点击运行exe.即可使用api调用使用。



## 调用

html中调用：，选择一个exe安装的模型名字，gemma3:1b  填入问题。 注意 跨域，本地测试使用编辑器开启前端服务访问。



![](.\img\2.png)

## 注意

需要注意的是： 小模型的逻辑和常识可能错误。

![](.\img\3.png)



## demo代码

本地流式 API的调用，查看官网的api调用示例。本例使用的是本地流式调用

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Ollama 本地 API 调用 Demo</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        body {
            max-width: 900px;
            margin: 30px auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .container {
            background: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h2 {
            color: #333;
            margin-top: 0;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 6px;
            font-weight: bold;
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
        }
        textarea {
            min-height: 100px;
            resize: vertical;
        }
        .btn-group {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            background: #007bff;
            color: white;
            font-size: 15px;
            cursor: pointer;
        }
        button:hover {
            background: #0056b3;
        }
        .result-box {
            border: 1px solid #ddd;
            border-radius: 6px;
            padding: 15px;
            min-height: 150px;
            white-space: pre-wrap;
            background: #fafafa;
        }
        .tip {
            color: #666;
            font-size: 13px;
            margin-top: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>本地 Ollama API 调用 Demo</h2>
        <p class="tip">确保 Ollama 已启动：ollama run 模型 / 直接保持 ollama 服务运行</p>

        <div class="form-group">
            <label>模型名称（例如：qwen2, llama3, gemma, phi）</label>
            <input type="text" id="model" value="qwen2" placeholder="输入你本地已拉取的模型">
        </div>

        <div class="form-group">
            <label>提问内容</label>
            <textarea id="prompt" placeholder="输入你想问 AI 的问题"></textarea>
        </div>

        <div class="btn-group">
            <button onclick="sendQuestion()">发送提问</button>
            <button onclick="loadTestSample()">加载测试样例</button>
        </div>

        <div class="form-group">
            <label>返回结果：</label>
            <div id="result" class="result-box">等待请求...</div>
        </div>
    </div>

    <script>
        // 加载测试样例
        function loadTestSample() {
            document.getElementById('prompt').value = `你好，请用简洁的语言介绍一下人工智能是什么，适合新手理解的版本。`;
            document.getElementById('result').innerText = "测试样例已加载，点击【发送提问】即可调用";
        }

        // 发送请求到本地 Ollama API
        async function sendQuestion() {
            const model = document.getElementById('model').value.trim();
            const prompt = document.getElementById('prompt').value.trim();
            const resultBox = document.getElementById('result');

            if (!model || !prompt) {
                resultBox.innerText = "⚠️ 请填写模型名称和提问内容";
                return;
            }

            resultBox.innerText = "⏳ 请求中，请稍候...\n";

            try {
                // 调用 Ollama 本地流式 API
                const response = await fetch('http://localhost:11434/api/generate', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        model: model,
                        prompt: prompt,
                        stream: true
                    })
                });

                const reader = response.body.getReader();
                const decoder = new TextDecoder();
                let fullResult = "";

                // 读取流式返回
                while (true) {
                    const { done, value } = await reader.read();
                    if (done) break;

                    // 解析每一行 JSON
                    const chunk = decoder.decode(value, { stream: true });
                    const lines = chunk.split('\n').filter(line => line.trim() !== '');

                    for (const line of lines) {
                        try {
                            const data = JSON.parse(line);
                            if (data.response) {
                                fullResult += data.response;
                                resultBox.innerText = fullResult;
                            }
                        } catch (e) {}
                    }
                }

                resultBox.innerText = fullResult + "\n\n✅ 请求完成";

            } catch (error) {
                resultBox.innerText = "❌ 调用失败：\n" + error.message + "\n请检查：\n1. Ollama 是否启动\n2. 模型是否已拉取\n3. 端口是否为 11434";
            }
        }
    </script>
</body>
</html>
```

