# 中国金融工具集

一套专为中国金融数据分析设计的 Claude Code 插件集合。

[![Codex 安装指南](https://img.shields.io/badge/Codex-安装指南-blue)](./INSTALL.md)

## 快速开始

- **Claude Code 用户**：使用 `/plugin` 命令一键安装（推荐）[查看详情](#claude-code推荐)
- **Codex CLI 用户**：查看详细的 [安装指南](./INSTALL.md)

## 插件列表

| 插件                               | 说明                                             |
| ---------------------------------- | ------------------------------------------------ |
| [cninfo-mcp](./plugins/cninfo-mcp) | 通过 MCP 协议从巨潮资讯查询和下载A股上市公司年报 |
| [pdf2docx-mcp](./plugins/pdf2docx-mcp) | 通过 MCP 协议将 PDF 文件转换为可编辑 DOCX 格式 |

## 技能列表

| 技能 | 说明 | 依赖插件 |
| ---- | ---- | -------- |
| [annual-report-benchmark](./skills/annual-report-benchmark) | 多公司年报财务对标取数，产出可复核 Excel | cninfo-mcp, pdf2docx-mcp |

## 安装方式

### Claude Code（推荐）

将本 Marketplace 添加到 Claude Code：

```
/plugin marketplace add youhaozhao/china-fin-toolkit
```

然后安装插件：

```
/plugin install cninfo-mcp@china-fin-toolkit
/plugin install pdf2docx-mcp@china-fin-toolkit
```

安装技能：

```
/plugin install annual-report-benchmark@china-fin-toolkit
```

### Codex CLI

 **查看详细的 [Codex 安装指南](./INSTALL.md)**

该指南包含：
- MCP Servers 配置（使用 npm 包，简单快捷）
- Skills 安装步骤
- 验证与故障排查
- 使用示例

> **提示**：你也可以直接让 Codex 帮你配置！在 Codex 中运行：
>
> ```
> 我正在配置 Codex 使用 china-fin-toolkit 插件包，项目地址是 https://github.com/youhaozhao/china-fin-toolkit，请帮我配置 MCP Servers 和 Skills。
> ```

## 许可证

MIT
