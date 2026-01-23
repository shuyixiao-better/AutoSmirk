# AutoSmirk

AutoSmirk —— 舒一笑不秃头的 Claude 编码默契契约。让 AI 记住你的习惯，省下千言万语，只留得意一笑 😏

## 🌿 仓库故事
我是 舒一笑不秃头，一个写代码也写诗的人。

在和 Claude 日复一日的协作中，我发现自己总在重复：“用 React + TS”、“加中文注释”、“别用 any”、“生成完整可运行组件”……
这些琐碎的叮嘱，像尘埃一样覆盖了创造的光芒。

于是，我写了 AutoSmirk —— 一份属于我的“AI 编码默契契约”。
它封装了我的技术栈偏好、代码风格、甚至对“好代码”的定义。
当我调用 @autosmirk，Claude 就会自动进入“懂我模式”，输出如诗般契合我心意的代码。

为什么叫 Smirk？
因为每次它精准命中我的需求时，我都会忍不住——得意一笑。
而“不秃头”，是我对高效、优雅、不内耗开发的坚持。

这不仅是一个 Skill，更是我对 Agentic Coding 的一次温柔实践：
让机器适应人，而不是让人迁就机器。

如果你也厌倦了重复解释，欢迎 Star、Fork，或带着你的“smirk”加入这场静默的革命。

## 🌍 English Intro (Optional)
I’m Shu Yixiao Butu Tou (yes, “Laughing Shu, Not Bald”) — a developer who believes code should read like poetry.

Tired of repeating the same instructions to Claude? Meet AutoSmirk: my personal coding covenant with AI.
It encodes my stack, style, and standards so I can focus on creation — not configuration.

The name? Every time Claude nails it… I smirk. 😏

## 📦 Project Layout
```
AutoSmirk/
├── SKILL.md                              # Skill 定义与使用契约
├── README.md                             # 项目说明文档
├── .ai-code-tracking.json                # AI 编码追踪配置
├── assets/                               # 视觉素材、Logo、演示媒体
├── references/                           # 参考文档与研究笔记
│   ├── frontmatter-tags-mapping.md       # Front Matter 标签智能映射配置
│   └── frontmatter-implementation.md     # Front Matter 生成逻辑参考
├── scripts/                              # 打包或验证辅助脚本
└── examples/                             # 示例提示词或输出
```

## ✅ Getting Started

### 安装 Skill

1. **克隆仓库**
   ```bash
   git clone https://github.com/shuyixiao-bututou/AutoSmirk.git
   cd AutoSmirk
   ```

2. **配置 Claude Code**

   在 Claude Code 的配置中添加此 skill 路径，或直接使用 `@autosmirk` 引用。

### 使用方式

#### 1. API 文档分析（Firecrawl）
```
@autosmirk analyze https://api.example.com/docs
```

#### 2. Front Matter 生成（VitePress）
```
# 单个文件
@autosmirk fm docs/article.md

# 目录批量处理
@autosmirk fm docs/articles

# 当前文件
@autosmirk fm
```

**生成示例**：
```yaml
---
layout: doc
title: Spring Security 实现 JWT 认证与授权
description: >-
  本文详细介绍如何使用 Spring Security 6 实现 JWT 认证，包括用户登录、令牌生成、权限验证等完整流程。
date: '2026-01-23'
tags:
  - Spring Boot
  - Spring Security
  - 认证鉴权
  - JWT
author: 舒一笑不秃头
---
```

#### 3. 复杂编码任务（Logic-First 确认）
```
@autosmirk build a React + TS client for this API
```

**流程**：AI 会先展示逻辑大纲，确认后才开始编码。

### 核心功能

| 功能 | 触发方式 | 说明 |
|------|----------|------|
| **API 分析** | `@autosmirk analyze <url>` | 使用 Firecrawl 爬取 API 文档并总结 |
| **Front Matter** | `@autosmirk fm <path>` | 为 Markdown 生成 VitePress YAML front matter |
| **逻辑优先** | 复杂任务自动触发 | 编码前先展示逻辑大纲，确认后执行 |
| **默认规范** | 所有 `@autosmirk` 任务 | 应用默认技术栈和代码风格偏好 |

## 🧩 Development Notes

### 技术栈偏好

- **前端**：React + TypeScript
- **后端**：Spring Boot / Node.js
- **类型**：避免 `any`，使用显式类型
- **注释**：仅对非平凡逻辑块添加简洁中文注释
- **输出**：提供完整可运行的组件或文件

### 代码风格

- 使用现代 ES6+ 语法
- 组件采用函数式 + Hooks
- 文件命名采用 kebab-case
- 导入顺序：第三方库 -> 内部模块 -> 类型导入

### 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'feat: add amazing feature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request
