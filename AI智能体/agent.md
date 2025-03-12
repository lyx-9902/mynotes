# AlAgent

## 简介：

###  什么是Agent

Agent:概念起源于哲学，描述了一种拥有欲望、信念、意图以及采取行动能力的实体。

###  什么是AlAgent

在人工智能领域这一术语被赋予了一层新的含义:具有自主性、反应性、交互性等特征的智能“代理”

### LLM based Al Agent

应用了大模型(LLM)能力的AIAgent.



特点：具象化，狭义化

## AlAgent的分类

**按照数量分：**

单Agent ：做单一任务  例如 查天气，Emoji翻译器；

多Agent： 多个单一agent，协调工作。

**按照属性分：**

![](.\img\1.png)

AI社会，多个AI组成的社区，一个AI发起举办party,到时间 AI邻居到场。



**按照自主程度分：**

![](.\img\2.png)

**按照行业应用分：**

![](.\img\3.png)



**Anthropic 内部分类**

>Anthropic内部分类 *Anthropic*是一家位于美国加州旧金山的人工智能初创公司，成立于2021年
>√工作流
>√智能体
>Anthropic对Agent的定义:Agent是一种代理系统，其中大语言模型(LLM)可以动态地指导自己的流程和工具使用，并控制如何完成任务，而不是 LLM 简单的衍生物。

![](.\img\4.png)

工作流：是用户输入参数，按照流程调用接口，返回内容。  特点：可靠性较高，自主性较低。

智能体： 输入参数，自行计算，调正参数，直到输出结果。  特点：可靠性较低，自主性较高。



Al Agent的现实意义

对于个体--超级个体

对于公司--数字员工

对于产品--形态重构
<img src=".\img\5.png" style="zoom:50%;" />



## Al Agent的核心组件

### **感知模块**

感知模块--多模态

（文本）（文字，表格，文档等)
(视觉)(图片，视频等)
I听觉(语音，音频文件等)
其他(触觉，嗅觉，距离，温度等)

### **大脑模块**

 知识、记忆、规划等

**a知识**(内置知识、外置知识)

内置知识:  常识知识,  专业知识,  语言知识

外置知识: 向量数据库,关系型数据库,知识图谱

**b记忆**(短期记忆、长期记忆)

短期记忆: 对话内容,系统级提示

长期记忆: 总结 ,RAG

**c规划**(CoT、ReAct、Plan and Execute、 Reflexion.....)

  思维链 ：CoT ToT ReAct

<img src=".\img\6.png" style="zoom:50%;" />

<img src=".\img\7.png" style="zoom:80%;" />

### 行动模块

工具调用： 阅读51个网页
具身行动： 执行动作



Al Agent的图种设计范式

(Reflection)反思
(Tool use)工具调用
(Planning)规划
(Multi-Agent)多智能体协作



### Al Agent的构建方式

**Agent平台**

字节跳动的扣子；

dify： https://cloud.dify.ai

FastGPT https://tryfastgpt.ai/zh

**代码构建**

<img src=".\img\8.png" style="zoom:80%;" />



## Agent的基本功

1.提示词 2. 示例 3.使用分隔符清楚地指示输入的不同部分

4.结构化表达 （角色，背景，目标，约束条件，目的）

## Agent目前的挑战和机遇

<img src=".\img\9.png" style="zoom:80%;" />



## AlAgent的终极目标:--AGI

通用人工智能（Artificial General Intelligence）

通往人工通用智能的道路，宛如一场旅程而非终点，但我相信Agent能帮助我们在这条漫长征途上迈出微小而坚实的一步。   ----吴恩达

# 第二课Coze+DeepSeek实现小红书爆款笔记 ，打造专属Agent智能体

了解主流Agent平台

熟悉Coze平台

掌握将DeepSeek接入Coze平台的方法

掌握Coze中的“工作流”和”插件”

理解Agent核心模块和工作流、插件之间的关系



<img src=".\img\10.png" style="zoom:80%;" />





<img src=".\img\11.png" style="zoom:70%;" />



<img src=".\img\12.png" style="zoom:70%;" />



<img src=".\img\13.png" style="zoom:70%;" />





### 2种模式对比

>单Agent(LLM模式)和单Agent(对话流模式)
>
>‌**LLM（Large Language Model）模式**‌是指大型语言模型在多智能体系统中的协作模式

LLM模式： 查询时，有一个前置模型过滤判断，内容不相关，不会访问自己的工作流。

对话流： 直接访问，不拦截。

区别： 输入变量名，有区别。

