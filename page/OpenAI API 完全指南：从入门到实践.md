## 简介

OpenAI API 是一个强大的工具，可以帮助开发者将 AI 能力集成到自己的应用中。本指南将帮助你从零开始，掌握 OpenAI API 的使用。

## 获取 API Key

### OpenAI 账号注册

如果你已经使用过 ChatGPT，可以直接使用该账号。新用户需要在 OpenAI 官网注册账号。

### 创建 API Key

1. 登录后，在左侧菜单找到 "API Keys"
2. 点击 "Create new secret key"
3. 为新 Key 命名并创建
4. **重要：** 立即保存显示的 Key，因为它只会显示一次

## 额度管理

### 查看使用情况

在 Usage 页面可以查看：
- 每日消费统计
- 额度状态（未使用/已使用/已过期）
- 使用记录

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

### 充值流程

1. 进入 Billing 页面
2. 添加支付方式
3. 返回 Overview 页面进行充值
4. 在 Usage 页面确认额度更新

## Python 开发配置

### 环境要求

- Python 3.7.1 或更高版本
- 建议使用 Anaconda 创建虚拟环境

### 安装依赖

python
pip install openai


### 配置 API Key

两种方式：

1. **全局配置：**
bash
# 添加系统环境变量 OPENAI_API_KEY


2. **项目配置：**
bash
# 在项目根目录创建 .env 文件
OPENAI_API_KEY=你的API Key


### 基础使用示例

python
from openai import OpenAI

client = OpenAI()

response = client.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "你是一位专业的助手"},
        {"role": "user", "content": "请介绍 OpenAI API"}
    ]
)

print(response.choices[0].message.content)


## 核心功能

### 文本生成

支持多种对话角色：
- system：设置 AI 行为
- user：用户输入
- assistant：AI 回复

### GPT-4 Vision

- 支持图像理解
- 可设置图像处理质量
- 支持多图像输入

### JSON 输出

python
response = client.chat.completions.create(
    model="gpt-3.5-turbo",
    response_format={"type": "json_object"},
    messages=[...]
)


## 实用提示

1. **安全性：**
   - 妥善保管 API Key
   - 设置使用限额
   - 定期检查使用情况

2. **性能优化：**
   - 合理设置 token 限制
   - 选择适当的模型版本
   - 缓存常用响应

3. **错误处理：**
   - 实现请求重试机制
   - 监控 API 响应状态
   - 做好异常处理

通过本指南，你应该能够开始使用 OpenAI API 进行开发。记住要经常查看官方文档以获取最新更新和更详细的信息。

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)