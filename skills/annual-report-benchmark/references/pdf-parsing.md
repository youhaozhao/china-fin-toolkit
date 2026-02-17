# 年报解析标准（单一最佳方案）

## 1. 唯一解析路径

- 只允许：`PDF -> DOCX`（使用 `pdf2docx-mcp`）
- 从 DOCX 文件中提取文本和表格数据进行字段识别

## 2. 执行要求

- 每份 PDF 仅转换一次
- 后续取数仅基于生成的 DOCX 文件

## 3. MCP 工具使用

使用 `pdf2docx-mcp` 提供的转换工具：

- `mcp__plugin_pdf2docx-mcp_pdf2docx-mcp__convert` - 执行 PDF 到 DOCX 转换
- `mcp__plugin_pdf2docx-mcp_pdf2docx-mcp__get_info` - 获取 PDF 元信息（页数完整性验证）

## 4. 最低验收

DOCX 中必须命中：

- 章节关键词：`主要会计数据和财务指标`
- 核心字段：`营业收入`、`归属于母公司股东的净利润`、`经营活动产生的现金流量净额`、`合同负债`

## 5. 失败处理

- 若最低验收未通过，当前 PDF 判定失败
- 进入缺失占位 + 原因说明流程，不得再次重试
