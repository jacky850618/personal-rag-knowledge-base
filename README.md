# KnowBase - 私人 RAG 知识库系统(让你的知识不再沉睡！)

![Python](https://img.shields.io/badge/Python-3.12-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-1.52-red)
![LangChain](https://img.shields.io/badge/LangChain-1.1-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

一个完全**本地运行**、**极致隐私**的个人 RAG（Retrieval-Augmented Generation）知识库系统。  
将你的 PDF、报告、笔记、书籍上传后，即可通过自然语言提问，获得精准、带原文出处的智能回答。

**核心亮点**：支持 PDF 中的**表格智能提取**和**图片内容描述**，全部使用本地模型，无需任何云服务！
## 📸 系统截图

### 智能问答页面
![智能问答](screenshots/s1.png)

### 知识库管理后台（文档上传、分页搜索、删除）
![知识库管理后台](screenshots/s2.png)

### 系统设置页面（多模型切换、代理配置、连接测试）
![系统设置页面](screenshots/s3.png)

## 🌟 核心功能

- **100% 本地运行 & 隐私保护**  
  所有文档、向量数据库、模型推理都在你的电脑上完成，数据永不离开本地。

- **深度理解 PDF 内容**  
  - **表格解析**：自动将 PDF 中的表格转为清晰 Markdown 格式，AI 可直接阅读并回答“表格里 Q3 收入是多少？”等问题  
  - **图片描述**：使用本地 BLIP 模型自动生成图片内容描述（如“一张柱状图显示2024年各季度销售额”），支持提问图片含义

- **高精度语义检索**  
  基于 BGE 嵌入模型，实现精准语义匹配，即使问题表述不同也能找到相关内容。

- **多大模型随意切换**  
  一键切换 DeepSeek、OpenAI (ChatGPT)、Groq、Claude、Gemini，永远用当时最强的模型。

- **优雅的 Web 界面**（Streamlit）  
  - 首页直接进入智能问答  
  - 管理后台：文档上传、分页搜索、预览、删除

- **开箱即用**  
  几分钟部署，首次运行自动下载所需模型，后续秒开。

## 🎯 最适合的场景

处理大量带表格的报告（财报、科研论文、市场分析、项目总结）
管理图文并茂的文档（产品手册、教程、会议记录、设计稿）
快速查询 PDF 中的具体数据、图表含义或图片内容
知识工作者、学生、研究员、产品经理、咨询顾问、投资爱好者

## 🚀 快速开始

### 1. 克隆仓库
```bash
git clone https://github.com/jacky850618/KnowBase.git
cd KnowBase
```

### 2. 安装依赖（推荐新建虚拟环境）
#### 安装 Poppler
1. macOS（最简单）
```
brew install poppler
```

2. Windows
```
conda install -c conda-forge poppler
```

3. Linux（Ubuntu/Debian）
```
sudo apt update
sudo apt install poppler-utils
```

#### 安装依赖
```
pip install -r requirements.txt
```

### 3. （中国大陆用户）加速下载嵌入模型
```
export HF_ENDPOINT=https://hf-mirror.com
```

### 4. 启动应用

```
streamlit run app.py
```

打开浏览器访问 http://localhost:8501，即可开始使用！

首次运行会自动下载：
1. BGE 嵌入模型（~1GB）
1. BLIP 图片描述模型（~1GB）
1. Table Transformer 表格检测模型（~400MB）
后续启动即秒开。

## 📁 项目结构
```
.
├── app.py                  # 主界面（智能问答 + 管理后台）
├── config_manager.py       # 持久化配置管理
├── knowledge_manager.py    # 知识库 CRUD 逻辑
├── embeddings.py           # 嵌入模型封装
├── data/                   # 上传的原始文档
├── chroma_db/              # 向量数据库（自动生成）
├── config/user_settings.json # 永久保存的配置（模型、Key、代理）
└── requirements.txt
```

## 配置说明
1. 在【管理后台 → 系统设置】填写你的大模型 API Key
1. 支持代理：填写主机、端口、协议（http/https/socks5）
1. 配置自动永久保存到 config/user_settings.json

## 🔧 技术亮点
1. 表格解析：Table Transformer（Microsoft）检测表格结构 + EasyOCR 本地识别文字 → 高精度 Markdown 输出
1. 图片理解：BLIP（Salesforce）大型模型生成自然语言描述，支持图表、截图、照片等
1. 文档切分：智能切块 + 附加表格/图片 chunk，确保上下文完整
1. 完全本地：无任何云 API 调用解析内容，隐私极致安全

## 🤝 贡献
欢迎 Star、Fork、Issue、PR！
未来计划：
1. 多轮对话历史s
1. 更多本地多模态模型支持
1. 文档自动摘要与标签
1. 移动端访问

## 开源协议
MIT License - 随意使用、修改、商用均可。