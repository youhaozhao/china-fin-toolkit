# 中国金融工具集

一套专为中国金融数据分析设计的 Claude Code 插件集合。

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

## 许可证

MIT
