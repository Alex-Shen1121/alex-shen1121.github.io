# AGENTS.md - 代理编码指南

本文档为在此仓库中运行的代理编码 agents 提供指导方针。

## 项目概述

使用 HugoBlox Academic CV 主题构建的 Hugo 静态学术网站，部署到 GitHub Pages。

- **Hugo 版本**：0.119.0（需要 Extended 版本以支持 SCSS/Sass）
- **Go 模块**：`github.com/HugoBlox/theme-academic-cv`

---

## 构建命令

### 本地开发

```bash
# 开启实时重载的本地开发服务器
hugo server

# 显示草稿内容
hugo server -D

# 指定端口
hugo server -p 1313
```

### 生产构建

```bash
# 生产环境构建
hugo --minify

# 指定环境变量
HUGO_ENVIRONMENT=production hugo --minify
```

### 验证

```bash
# 完整构建检查（包含未来内容）
hugo --buildFuture

# 检查配置
hugo config

# 列出内容并显示警告
hugo --printPathWarnings --printUnusedTemplates
```

注意：Hugo 没有传统的单元测试。验证通过构建检查完成。

---

## 代码风格指南

### 编辑器配置

遵循 `.editorconfig`：

- **字符集**：UTF-8
- **行尾符**：LF（Unix）
- **缩进**：2 空格
- **尾部空格**：去除
- **末尾换行**：保留

### YAML 头部信息

```yaml
---
title: "您的标题"
date: '2024-01-15'
summary: "简短描述"
tags:
- 标签1
- 标签2
featured: false
---
```

规则：
- 使用 `---` 分隔符独立成行
- 日期：ISO 8601 格式（`YYYY-MM-DD`）
- 布尔值：小写（`true`/`false`）
- 字符串：仅在需要时加引号

### Markdown

- 标题：ATX 风格（`#`、`##`、`###`）
- 链接：描述性文字，内部链接优先使用相对路径
- 图片：放在同一文件夹或 `/images/`
- 短代码：`{{< >}}`（HTML）或 `{{% %}}`（Markdown）

### 命名规范

| 项目 | 规范 | 示例 |
|------|------|------|
| 文件夹 | kebab-case | `blog-post/` |
| 图片 | kebab-case | `featured-image.jpg` |
| 字段 | 小写 | `publishDate` |
| 标签 | kebab-case | `machine-learning` |

### 文件组织

```
content/
├── _index.md           # 章节索引
├── authors/            # 作者简介
├── event/              # 演讲/活动
├── post/               # 博客文章（content/post/<slug>/index.md）
├── publication/        # 出版物（content/publication/<type>/index.md）
├── project/            # 项目
└── slides/            # 演示文稿
```

---

## 错误处理

- **模板错误**：检查短代码语法和参数名
- **资源缺失**：验证头部信息中的文件路径
- **构建失败**：运行 `hugo --verbose` 查看详情

---

## 最佳实践

1. 推送前本地测试：`hugo server -D`
2. 使用描述性的提交信息
3. 优化图片（推荐 WebP）
4. 定期验证外部链接
5. 内部链接使用相对路径
6. 重大修改前备份内容

---

## 依赖

- **Hugo Extended**：>= 0.119.0
- **Go**：>= 1.15

更新 Hugo 版本：`.github/workflows/publish.yaml`（第 4 行）和 `netlify.toml`（第 6 行）

---

## CI/CD

推送到 `main` 分支时自动部署。详见 `.github/workflows/publish.yaml`。
