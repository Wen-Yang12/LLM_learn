# Langchain
Langchain是一个开源框架，相当于一个工具箱，帮开发者更方便地构建基于大语言模型的应用。它不是Agent本身，而是让Agent开发更顺手的工具集合。
## Langchain的作用
1. **连接外部数据**：Langchain能让LLM去查数据库、搜网页、调API，获取最新信息。
2. **记东西**：它能帮Agent记住对话的内容，即上下文。
3. **用工具**：LangChain能让LLM调用各种工具，例如计算器、天气API
4. **复杂任务拆解**：它能将大需求的任务拆分为各个小需求的小步骤，逐步解决

## Langchain与Agent的关系
Langchain好比Agent的万能工具箱，但没有那么万能，它只是提供了很大现成的模型。比如：
 - **链（Chains）**：把多个操作串起来，比如先理解用户的意图，再查数据，最后生成回答。比如 chat = llm | prompt
 - **工具（Tools）**:让Agent调用外部的功能，比如搜索、计算、翻译
 - **记忆（Memory）**：存储对话历史或用户数据
 - **检索（RAG）**：从知识库或网上抓取最新数据

## 举个例子
假如让Agent回答“明天北京天气咋样？”，Langchain可以：
1. 帮Agent理解你的问题（感知）
2. 决定调用天气API（决策）
3. 调用API查数据，再把结果整理成一句人话（行动），整个过程就像给Agent配了个工具箱，让它能自己找工具、干活。

## LLM应用

```
# 通义大模型
from langchain_community.llms import tongyi
key='自己的密钥'

llm = tongyi.Tongyi(api_key = key)

# 调用模型使用
info = llm.invoke("夏天适合吃什么水果？")
print(info)
```
```
# 智普AI
key = '自己的密钥'

from langcain_community.chat_models import ChatZhipuAI
from langchian_core.message import AIMessage,HumanMessage,SystemMessage

import os

os.environ["ZHIPUAI_API_KEY"] = key

chat = ChatZhipuAI(
  model = "glm-4",
  temperature = 0.5, # 模型温度,值在0-1之间，值越小，随机性越低
)

messages = [
  SystemMessage(content = "你是一个助手，请用中文回复"),
  HumanMessage(content = "夏天适合吃什么水果？")
]

response = chat.invoke(messages)
print(response.content)
```
