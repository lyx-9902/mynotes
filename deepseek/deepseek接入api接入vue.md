# deepeek接入vue3

 官方文档： https://api-docs.deepseek.com/zh-cn/



项目代码

```vue
  import OpenAI from 'openai';
  
  <MessageList :messages="messages" />
  
          <ChatControls 
            v-model="messageText"
            @send="sendMessage"
       />

<script setup>
const openai = new OpenAI({
  baseURL: 'https://api.deepseek.com',
  apiKey: 'sk-4d46c62091be480980f2a**40952a040f',
  dangerouslyAllowBrowser: true
});
const sendMessage = async () => {
  if (!messageText.value.trim()) return;

  addMessage(messageText.value, true);
  messages.value.push({ type: 'waiting' });
  
  const userInput = messageText.value;
  messageText.value = '';

  try {
    await fetchDeepSeekAPI(userInput);
  } catch (error) {
    addMessage('抱歉，请求出错，请重试', false);
  }
};

const fetchDeepSeekAPI = async (message) => {
  try {
    const completion = await openai.chat.completions.create({
      model: "deepseek-chat",
      messages: [
        { role: "system", content: "你是一个有帮助的助手" },
        { role: "user", content: message }
      ],
      stream: true,
      temperature: 0.7
    });

    let fullResponse = '';
    removeWaitingMessage();
    messages.value.push({ text: '', type: 'received' });
    
    for await (const chunk of completion) {
      const chunkContent = chunk.choices[0]?.delta?.content || '';
      if (chunkContent) {
        fullResponse += chunkContent;
        const lastMessage = messages.value[messages.value.length - 1];
        if (lastMessage && lastMessage.type === 'received') {
          lastMessage.text = fullResponse;
        }
      }
    }
    return fullResponse;
  } catch (error) {
    console.error('API请求失败:', error);
    throw error;
  }
};

// 恢复等待消息移除方法
const removeWaitingMessage = () => {
  const index = messages.value.findIndex(m => m.type === 'waiting');
  if (index > -1) messages.value.splice(index, 1);
};

const addMessage = (text, isSent) => {
  messages.value.push({ 
    text: text, 
    type: isSent ? 'sent' : 'received' 
  });
};

</script>
```



项目案例可参考：

https://gitee.com/yatlatic/51-world-demo/tree/master    