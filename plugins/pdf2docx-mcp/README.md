# pdf2docx-mcp

通过 MCP 协议将 PDF 文件转换为可编辑 DOCX 格式的 Claude Code 插件。

## 功能特性

- 将 PDF 文件转换为可编辑的 DOCX 格式
- 支持指定页码范围转换
- 支持加密 PDF（需提供密码）
- 获取 PDF 元信息（页数、作者、标题等）

## 安装方式

```
/plugin install pdf2docx-mcp@china-fin-toolkit
```

或通过 Marketplace 安装：

```
/plugin marketplace add youhaozhao/china-fin-toolkit
/plugin install pdf2docx-mcp@china-fin-toolkit
```

## 使用示例

安装完成后，即可在 Claude Code 中使用以下 MCP 工具：

### 转换 PDF 为 DOCX

> 把 /Users/me/report.pdf 转换成 DOCX

### 指定页码范围转换

> 将 /Users/me/report.pdf 的第 1-5 页转换为 DOCX，保存到 ~/output/

### 获取 PDF 元信息

> 获取 /Users/me/report.pdf 的页数和元信息

## MCP 服务

本插件通过 `npx` 运行 `@youhaozhao/pdf2docx-mcp`，无需额外安装依赖（Python 依赖会自动安装）。

## 系统要求

- Node.js 18+
- Python 3.10+

## 许可证

MIT
