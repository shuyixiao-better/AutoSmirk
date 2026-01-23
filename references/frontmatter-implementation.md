# Front Matter 生成逻辑参考

本文档描述 AutoSmirk front matter 生成功能的内部实现逻辑，供 Claude AI 参考。

## 核心数据结构

```typescript
interface FrontMatter {
  layout: string;      // 固定值 "doc"
  title: string;       // 文章标题
  description: string; // 文章描述
  date: string;        // ISO 格式日期
  tags: string[];      // 标签数组
  author: string;      // 作者名称
}
```

## 生成流程

### 1. 检测现有 Front Matter

```typescript
function hasFrontMatter(content: string): boolean {
  const trimmed = content.trimStart();
  return trimmed.startsWith('---');
}
```

**规则**：
- 如果文件已存在 `---` 开头，跳过处理
- 告知用户该文件已有 front matter

### 2. 提取标题 (title)

```typescript
function extractTitle(content: string): string {
  // 1. 提取第一个 # 标题
  const h1Match = content.match(/^#\s+(.+)$/m);
  if (h1Match) return cleanMarkdown(h1Match[1].trim());

  // 2. 提取第一个 ## 标题
  const h2Match = content.match(/^##\s+(.+)$/m);
  if (h2Match) return cleanMarkdown(h2Match[1].trim());

  // 3. 默认值
  return "未命名文档";
}

function cleanMarkdown(text: string): string {
  return text
    .replace(/\*\*(.+?)\*\*/g, '$1')  // 移除加粗
    .replace(/\*(.+?)\*/g, '$1')      // 移除斜体
    .replace(/`(.+?)`/g, '$1')        // 移除行内代码
    .replace(/\[(.+?)\]\(.+?\)/g, '$1') // 移除链接，保留文本
    .trim();
}
```

### 3. 提取描述 (description)

```typescript
function extractDescription(content: string): string {
  const lines = content.split('\n');
  const description: string[] = [];

  for (const line of lines) {
    const trimmed = line.trim();

    // 跳过空行、标题、代码块标记、引用、图片
    if (!trimmed ||
        trimmed.startsWith('#') ||
        trimmed.startsWith('```') ||
        trimmed.startsWith('>') ||
        trimmed.startsWith('!') ||
        trimmed.startsWith('-') && trimmed.startsWith('- ')) {
      continue;
    }

    // 跳过已经是 front matter 的内容
    if (trimmed === '---') continue;

    // 收集有意义的内容
    const cleaned = cleanMarkdown(trimmed);
    if (cleaned) {
      description.push(cleaned);
    }

    // 达到长度限制（约200字符）
    if (description.join(' ').length > 180) break;
  }

  let result = description.join(' ').trim();

  // 截断过长内容
  if (result.length > 200) {
    result = result.substring(0, 197) + '...';
  }

  return result || "暂无描述";
}
```

### 4. 生成日期 (date)

```typescript
function generateDate(): string {
  const now = new Date();
  const year = now.getFullYear();
  const month = String(now.getMonth() + 1).padStart(2, '0');
  const day = String(now.getDate()).padStart(2, '0');
  return `'${year}-${month}-${day}'`;  // 注意：YAML 需要引号
}
```

### 5. 推断标签 (tags)

```typescript
function inferTags(filePath: string, content: string): string[] {
  const pathLower = filePath.toLowerCase();
  const tags = new Set<string>();

  // 基于路径关键词推断
  for (const [keyword, tagList] of TAG_KEYWORDS) {
    if (pathLower.includes(keyword)) {
      tagList.forEach(tag => tags.add(tag));
    }
  }

  // 基于内容关键词推断（补充）
  const contentLower = content.toLowerCase();
  for (const [keyword, tagList] of TAG_KEYWORDS) {
    if (tags.size >= 5) break;  // 最多5个标签
    if (contentLower.includes(keyword) && !pathLower.includes(keyword)) {
      tagList.forEach(tag => tags.add(tag));
    }
  }

  // 转换为数组，限制数量
  const result = Array.from(tags).slice(0, 5);

  // 默认标签
  return result.length > 0 ? result : ['技术'];
}
```

**关键词映射（示例）**：
```typescript
const TAG_KEYWORDS = new Map<string, string[]>([
  ['java', ['Java']],
  ['spring', ['Spring Boot']],
  ['security', ['安全']],
  ['auth', ['认证鉴权']],
  ['jwt', ['JWT']],
  ['redis', ['Redis', '缓存']],
  ['algorithm', ['算法']],
  // ... 完整映射见 frontmatter-tags-mapping.md
]);
```

### 6. 生成 Front Matter

```typescript
function generateFrontMatter(
  title: string,
  description: string,
  date: string,
  tags: string[],
  author: string = '舒一笑不秃头'
): string {
  const yamlTags = tags.map(tag => `  - ${tag}`).join('\n');

  return `---
layout: doc
title: ${title}
description: >-
  ${description}
date: ${date}
tags:
${yamlTags}
author: ${author}
---`;
}
```

### 7. 写入文件

```typescript
function insertFrontMatter(content: string, frontMatter: string): string {
  // 移除文件开头的空行
  const trimmed = content.trimStart();
  return frontMatter + '\n\n' + trimmed;
}
```

## 完整处理流程

```
1. 读取文件内容
   ↓
2. 检查是否已有 front matter
   ├─ 有 → 跳过，告知用户
   └─ 无 → 继续
   ↓
3. 提取信息
   ├─ title: 从第一个 # 或 ## 标题
   ├─ description: 从首段有效文本
   ├─ date: 当前日期
   ├─ tags: 路径+内容关键词推断
   └─ author: 固定值
   ↓
4. 生成 front matter YAML
   ↓
5. 显示预览给用户
   ↓
6. 等待用户确认
   ├─ 确认 → 写入文件
   ├─ 取消 → 不操作
   └─ 修改 → 根据用户输入调整后写入
   ↓
7. 完成
```

## 目录处理模式

```typescript
async function processDirectory(dirPath: string) {
  const mdFiles = await glob('**/*.md', { cwd: dirPath });

  console.log(`发现 ${mdFiles.length} 个 Markdown 文件`);

  for (const file of mdFiles) {
    await processFile(path.join(dirPath, file));
  }
}
```

## 错误处理

```typescript
interface ProcessResult {
  file: string;
  status: 'success' | 'skipped' | 'error';
  message?: string;
}

async function processFile(filePath: string): Promise<ProcessResult> {
  try {
    const content = await readFile(filePath, 'utf-8');

    if (hasFrontMatter(content)) {
      return { file: filePath, status: 'skipped', message: '已有 front matter' };
    }

    // ... 生成逻辑

    return { file: filePath, status: 'success' };
  } catch (error) {
    return { file: filePath, status: 'error', message: error.message };
  }
}
```

## 配置选项

```typescript
interface FrontMatterConfig {
  layout?: string;           // 默认 "doc"
  author?: string;           // 默认 "舒一笑不秃头"
  maxTags?: number;          // 默认 5
  descriptionLength?: number; // 默认 200
  defaultTags?: string[];    // 默认 ['技术']
}
```

## 预览模板

```
┌─────────────────────────────────────────────────────────────┐
│  Front Matter 预览                                          │
├─────────────────────────────────────────────────────────────┤
│ ---                                                         │
│ layout: doc                                                 │
│ title: Spring Security 实现 JWT 认证与授权                   │
│ description: >-                                            │
│   本文详细介绍如何使用 Spring Security 6 实现 JWT 认证...    │
│ date: '2026-01-23'                                         │
│ tags:                                                       │
│   - Spring Boot                                            │
│   - Spring Security                                        │
│   - 认证鉴权                                               │
│   - JWT                                                    │
│ author: 舒一笑不秃头                                         │
│ ---                                                         │
├─────────────────────────────────────────────────────────────┤
│ 推断依据:                                                   │
│ - 标题来源: 第一个 # 标题                                    │
│ - 标签来源: 路径关键词 spring, security, auth                │
├─────────────────────────────────────────────────────────────┤
│ 是否写入文件？(确认/取消/修改)                                │
└─────────────────────────────────────────────────────────────┘
```
