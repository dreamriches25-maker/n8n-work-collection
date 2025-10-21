# Poem Shorts - 中国古典诗词短视频生成项目

## 项目概述

Poem Shorts 是一个基于 n8n 工作流的自动化系统，能够将中国古典诗词自动转化为短视频内容。项目通过 AI 技术生成视频脚本、图片素材，并最终合成具有专业效果的短视频。

## 功能特点

- 📝 **智能脚本生成**：使用 DeepSeek AI 生成诗词分镜脚本
- 🎨 **AI 图片生成**：基于 Gemini 2.0 生成中国古风卡通风格的图片
- 🎬 **自动视频合成**：通过 MoneyPrinterPro API 生成专业短视频
- 📊 **云端集成**：与 Google Drive、Google Sheets 无缝集成
- 🚀 **全自动化**：从诗词输入到视频发布的全流程自动化

## 技术架构

### 核心组件

1. **AI 模型服务**DeepSeek V3.1 (通过 OpenRouter)：脚本和提示词生成Google Gemini 2.0 Flash：图片生成MoneyPrinterPro：视频合成
2. **云服务集成**Google Drive：文件存储和管理Google Sheets：数据记录和追踪YouTube：视频发布平台
3. **工作流引擎**n8n：自动化工作流编排

## 工作流程

### 第一阶段：图片资源生成

1. **用户输入**诗词标题、作者、类型、文件夹名称
2. **内容准备**获取诗词原文内容创建本地存储文件夹
3. **脚本生成**生成视频分镜脚本保存到 Google Sheets
4. **图片提示词生成**基于分镜脚本生成中英文图片提示词提取英文提示词用于图片生成
5. **图片生成**调用 Gemini API 生成图片按顺序命名并保存到本地和 Google Drive

### 第二阶段：视频生成

1. **资源检查**扫描本地图片文件构建视频素材列表
2. **视频合成**调用 MoneyPrinterPro API监控生成进度下载最终视频文件
3. **发布准备**生成视频描述准备 YouTube 上传

## 安装和配置

### 前置要求

- n8n 实例（支持节点执行）
- Docker 环境（用于本地文件存储）
- 相关 API 密钥：OpenRouter API 密钥Google Cloud 凭证（Drive、Sheets、YouTube）MoneyPrinterPro API 访问

### 环境配置

1. **导入工作流**将提供的 JSON 文件导入 n8n
2. **配置凭证**设置 Google OAuth2 凭证配置 OpenRouter API 密钥设置 Gemini API 访问
3. **目录权限**确保 `/mnt/`目录有写权限配置正确的文件路径映射

## 使用说明

### 启动工作流

1. 通过表单触发器提供输入：诗词标题（如："早发白帝城"）作者（如："李白"）类型（如："唐诗"）文件夹名字（用于文件组织）
2. 工作流将自动执行：图片生成（约需几分钟）视频合成（时间取决于视频长度）
3. 最终输出：本地视频文件 (`/mnt/{文件夹名字}/{诗词标题}.mp4`)Google Drive 中的图片资源YouTube 视频（如配置了上传）

## 节点说明

### 关键节点功能

| 节点名称                         | 功能描述        |
| -------------------------------- | --------------- |
| `On form submission`             | 用户输入接口    |
| `PoemContent`                    | 获取诗词原文    |
| `AI Generate Video Clips Prompt` | 生成分镜脚本    |
| `AI Generate Images Prompts`     | 生成图片提示词  |
| `Generate an image`              | Gemini 图片生成 |
| `Call MoneyPrinterTurbo API`     | 视频合成        |
| `Upload a video`                 | YouTube 上传    |

### 自定义代码节点

- **Extract Prompt from AI Output**：从 AI 输出中提取英文提示词
- **Create Sequence Number for File Name**：生成序列化文件名
- **Create Request Body**：构建视频合成请求体

## 配置参数

### 视频参数

- 视频比例：9:16（竖屏）
- 剪辑模式：顺序播放
- 转场效果：淡入淡出
- 语言：中文
- 语音：zh-CN-YunyangNeural-Male

### 图片参数

- 风格：中国古风卡通
- 视角：第一人称航拍
- 色调：从晨光金黄到清朗碧蓝的渐变

## 故障排除

### 常见问题

1. **图片生成失败**检查 Gemini API 配额验证提示词格式
2. **视频合成错误**确认 MoneyPrinterPro 服务状态检查图片文件路径
3. **权限问题**验证 Google API 权限范围检查本地目录权限

### 日志查看

- 通过 n8n 执行历史查看详细日志
- 检查各节点的输入输出数据

## 扩展建议

1. **多诗词批量处理**
2. **自定义视觉风格**
3. **多平台发布支持**
4. **质量优化和缓存机制**

## 许可证

本项目仅供学习和个人使用。商业使用请确保遵守相关 API 的服务条款和版权规定。

## 支持

如遇到技术问题，请检查：

1. n8n 官方文档
2. 各 API 服务的状态页面
3. 工作流节点的配置说明

------

# Poem Shorts - Classical Chinese Poetry Short Video Generator

## Project Overview

Poem Shorts is an automated n8n workflow that transforms classical Chinese poetry into engaging short videos. The system leverages AI technologies to generate video scripts, create visual assets, and produce professional-quality video content automatically.

## Key Features

- 📝 **AI-Powered Script Generation**: Uses DeepSeek AI to create video storyboards
- 🎨 **AI Image Generation**: Creates Chinese ancient-style cartoon images using Gemini 2.0
- 🎬 **Automated Video Production**: Generates professional videos via MoneyPrinterPro API
- 📊 **Cloud Integration**: Seamless integration with Google Drive and Google Sheets
- 🚀 **End-to-End Automation**: Full pipeline from poetry input to video publication

## Technical Architecture

### Core Components

1. **AI Model Services**DeepSeek V3.1 (via OpenRouter): Script and prompt generationGoogle Gemini 2.0 Flash: Image generationMoneyPrinterPro: Video synthesis
2. **Cloud Services**Google Drive: File storage and managementGoogle Sheets: Data logging and trackingYouTube: Video publishing platform
3. **Workflow Engine**n8n: Automation workflow orchestration

## Workflow Process

### Phase 1: Image Asset Generation

1. **User Input**Poetry title, author, type, and folder name
2. **Content Preparation**Retrieve original poetry contentCreate local storage directory
3. **Script Generation**Generate video storyboard scriptSave to Google Sheets
4. **Image Prompt Generation**Create Chinese/English image prompts based on storyboardExtract English prompts for image generation
5. **Image Generation**Call Gemini API to generate imagesSave with sequential naming to local storage and Google Drive

### Phase 2: Video Generation

1. **Resource Validation**Scan local image filesBuild video material list
2. **Video Synthesis**Call MoneyPrinterPro APIMonitor generation progressDownload final video file
3. **Publication Preparation**Generate video descriptionPrepare for YouTube upload

## Installation & Configuration

### Prerequisites

- n8n instance (with node execution support)
- Docker environment (for local file storage)
- Required API keys:OpenRouter API keyGoogle Cloud credentials (Drive, Sheets, YouTube)MoneyPrinterPro API access

### Environment Setup

1. **Import Workflow**Import the provided JSON file into n8n
2. **Configure Credentials**Set up Google OAuth2 credentialsConfigure OpenRouter API keySet up Gemini API access
3. **Directory Permissions**Ensure write permissions for `/mnt/`directoryConfigure proper file path mappings

## Usage Instructions

### Starting the Workflow

1. Provide input via form trigger:Poetry title (e.g., "Early Departure from White Emperor City")Author (e.g., "Li Bai")Type (e.g., "Tang Poetry")Folder name (for file organization)
2. Workflow executes automatically:Image generation (takes several minutes)Video synthesis (duration depends on video length)
3. Final outputs:Local video file (`/mnt/{folder_name}/{poetry_title}.mp4`)Image assets in Google DriveYouTube video (if upload is configured)

## Node Descriptions

### Key Node Functions

| Node Name                        | Function Description             |
| -------------------------------- | -------------------------------- |
| `On form submission`             | User input interface             |
| `PoemContent`                    | Retrieve original poetry content |
| `AI Generate Video Clips Prompt` | Generate storyboard script       |
| `AI Generate Images Prompts`     | Create image prompts             |
| `Generate an image`              | Gemini image generation          |
| `Call MoneyPrinterTurbo API`     | Video synthesis                  |
| `Upload a video`                 | YouTube upload                   |

### Custom Code Nodes

- **Extract Prompt from AI Output**: Extract English prompts from AI response
- **Create Sequence Number for File Name**: Generate sequential filenames
- **Create Request Body**: Build video synthesis request payload

## Configuration Parameters

### Video Settings

- Aspect ratio: 9:16 (vertical)
- Clip mode: Sequential playback
- Transition effect: FadeIn
- Language: Chinese
- Voice: zh-CN-YunyangNeural-Male

### Image Settings

- Style: Chinese ancient cartoon
- Perspective: First-person aerial view
- Color scheme: Gradient from morning golden to clear blue

## Troubleshooting

### Common Issues

1. **Image Generation Failures**Check Gemini API quotaValidate prompt format
2. **Video Synthesis Errors**Verify MoneyPrinterPro service statusCheck image file paths
3. **Permission Problems**Validate Google API permission scopesCheck local directory permissions

### Logging

- View detailed logs through n8n execution history
- Examine input/output data for each node

## Extension Suggestions

1. **Batch Processing for Multiple Poems**
2. **Custom Visual Styles**
3. **Multi-platform Publishing Support**
4. **Quality Optimization and Caching Mechanisms**

## License

This project is for learning and personal use only. Commercial use must comply with relevant API service terms and copyright regulations.

## Support

For technical issues, please check:

1. n8n official documentation
2. API service status pages
3. Workflow node configuration guides

------

