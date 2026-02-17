---
name: annual-report-benchmark
description: |
  年报财务对标 - 使用 cninfo-mcp 对一组 A 股股票代码执行年度财务对标取数、指标计算和 Excel 输出。

  适用场景：
  - 年报财务数据提取与对比
  - 多公司财务指标对标分析
  - 经营质量评估（毛利率、净利率、周转率等）
  - 员工效率分析（人均营收、人均薪酬等）
  - 可复核的财务交付物生成

  触发关键词：财务对标、年报取数、财务比较、A股对比、经营质量分析、年报分析

  依赖：cninfo-mcp, pdf2docx-mcp
---

# 年报财务对标

## 目标

基于 `Y` 年与 `Y-1` 年年报，完成多公司可复核财务的取数和对标工作，产出 Excel 文件。

## 开工前读取（按顺序）

1. `references/required-fields.md`（唯一字段字典，23 项）
2. `references/pdf-parsing.md`（PDF 解析标准）
3. `references/extraction-rules.md`（取数流程与止损）
4. `references/metric-definitions.md`（公式与质量标记）
5. `references/excel-spec.md`（输出组织与命名）

## 执行流程

1. 接收参数：股票代码列表、报告期 `Y`（默认最新完整年报）。
2. 为每个代码下载 `Y` 与 `Y-1` 两份年报。
3. 每家公司独立处理，先完成单公司表，再处理下一家公司。
4. 解析路径固定：使用 `pdf2docx-mcp` 执行 `PDF -> DOCX` 转换，然后从 DOCX 提取内容。
5. 按字段字典提取、补算、打质量标记；同义词仅用于识别，输出名必须回填为字典名。
6. 单公司完成后执行 23 项覆盖校验；缺失项保留占位，不得删行。
7. 全部公司完成后，再聚合生成总对比表。
8. 按 `excel-spec` 生成最终 Excel；结论与数据质量说明写入 Excel 的 `03_说明` sheet，不另行输出文本。

## 硬性约束

- 每家公司最多 2 轮自动提取；第 2 轮失败必须降级。
- 降级产物必须包含：单公司对比表（可提取字段）+ 缺失项清单 + 失败原因；降级产物视为已产出单公司表。
- 未产出当前公司单公司表（含降级表），不得进入下一家公司或总表聚合。
- 全部交付物写入同一个 Excel 文件，不另行输出其他格式。

## 参考文件

- 提取流程与字段映射：`references/extraction-rules.md`
- 指标定义与公式：`references/metric-definitions.md`
- 必填字段字典：`references/required-fields.md`
- PDF 解析标准：`references/pdf-parsing.md`
- Excel 规范：`references/excel-spec.md`

## MCP 工具

本技能依赖以下 MCP 工具。**执行前必须确认这两个 plugin 已在当前环境中可用。若未发现，立即停止并告知用户执行以下命令安装后再重新启动任务，不得继续执行：**

```
/plugin install cninfo-mcp@china-fin-toolkit
/plugin install pdf2docx-mcp@china-fin-toolkit
```

### cninfo-mcp

- `mcp__plugin_cninfo-mcp_cninfo-mcp__query_annual_reports_tool` - 查询年报信息
- `mcp__plugin_cninfo-mcp_cninfo-mcp__download_annual_reports_tool` - 下载年报 PDF

### pdf2docx-mcp

- `mcp__plugin_pdf2docx-mcp_pdf2docx-mcp__convert` - 转换 PDF 格式的年报到 DOCX 格式
- `mcp__plugin_pdf2docx-mcp_pdf2docx-mcp__get_info` - 获取 PDF 元信息用于验证转换的完整性
