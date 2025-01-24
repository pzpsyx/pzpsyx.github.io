## 获得 OpenAI API Key

### 获得 OpenAI 账号

如果之前使用过 ChatGPT，那么 ChatGPT 的账号就是 OpenAI 账号，可以直接使用。

如果没有账号，可以在 OpenAI 官网注册。由于国内访问限制，注册可能较为复杂，可以参考网上的教程，或者直接购买现成的账号或 API Key。

### 获取 OpenAI API Key

登录后，将鼠标移动到页面左侧，会弹出一个侧边栏。

点击侧边栏中的 **“API Keys”** 进入 API Keys 页面。在这里可以管理（创建、删除等）所有的 API Key。

点击 **“Create new secret key”** 创建新的 API Key，进行命名并确认。随后会弹出一个对话框，显示新创建的 Key。请务必立即保存该 Key，因为关闭对话框后将无法再次查看。

保存完成后，点击 **Done**，即可在页面中看到新创建的 API Key。

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

## 获取 API 使用额度

### 额度查询

点击侧边栏中的 **“Usage”** 进入使用页面。

页面左侧显示每日花费，右侧显示额度。在 **Credit Grants** 区域，额度状态分为三种颜色：
- **灰色**：未使用；
- **绿色**：已使用；
- **红色**：已过期。

只有未使用状态（灰色）的额度，才能成功调用 API。

### 额度充值

点击侧边栏中的 **“Setting”** 下的 **“Billing”** 进入账单页面。在此页面可以管理充值相关事项。

首先需要添加一种付款方式，点击 **Payment methods** 进行管理。由于国内支付限制，可以选择使用国外的信用卡或虚拟卡。

推荐使用 [野卡](https://bit.ly/bewildcard)，支持便捷的支付方式，适合充值需求。

添加支付方式后，回到 **Overview** 页面，点击 **Add to credit balance** 即可完成充值。充值完成后，回到 **Usage** 页面即可查看额度变化。

## Python 使用测试

### 配置 Python 环境

确保 Python 版本为 3.7.1 以上。建议使用 Anaconda 创建虚拟环境以便管理依赖。

### 安装 OpenAI 库

使用以下命令安装 OpenAI 库：

bash
pip install openai


### 设置你的 API Key

OpenAI 默认从环境变量中读取 `OPENAI_API_KEY`，可以通过以下两种方式设置：

1. **为所有项目设置**  
   在系统环境变量中添加 `OPENAI_API_KEY`。完成后，可以通过命令行运行以下命令检查是否设置成功：
   bash
   echo %OPENAI_API_KEY%
   

2. **为单个项目设置**  
   在项目文件夹中创建 `.env` 文件（注意将其加入 `.gitignore` 以防泄露），内容如下：
   env
   OPENAI_API_KEY=你的APIKey
   

### 发送请求测试

以下是一个简单的 GPT-3.5 Chat 请求示例：

python
import os
import openai
from dotenv import load_dotenv

load_dotenv()

openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a poetic assistant, skilled in explaining complex programming concepts with creative flair."},
        {"role": "user", "content": "Compose a poem that explains the concept of recursion in programming."}
    ]
)

print(response['choices'][0]['message']['content'])


运行后，可以在 [Usage 页面](https://platform.openai.com/usage) 查看请求的花费和 token 数量。

## 功能介绍（以 Python 为例）

### 文本生成（Text Generation）

官方教程：[OpenAI 文本生成指南](https://platform.openai.com/docs/guides/text-generation)

OpenAI 的 GPT 模型可以理解语言（GPT-4 还支持图像输入），并返回文字结果。以下是一个简单的对话示例：

python
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)

print(response['choices'][0]['message']['content'])


主要输入参数为 `messages`，它是一个包含多个消息对象的列表。每个消息对象由以下部分组成：
- **system**（可选）：设置 AI 的行为；
- **user**：用户输入；
- **assistant**：AI 的回复。

每次回复中都会包含一个 `finish_reason`，表示回复的完成状态：
- **stop**：正常完成；
- **length**：达到最大 token 限制；
- **tool_call**：调用工具；
- **content_filter**：内容被过滤；
- **null**：尚未完成。

### 图像生成（Image Generation）

GPT-4 的 vision 版本支持图像输入和生成。可以通过在 `user` 消息中添加 `type` 为 `image_url` 的图像 URL 来实现。

---

以上是 OpenAI API 的基础使用方法和功能介绍。通过合理配置和使用，可以高效完成各种任务。