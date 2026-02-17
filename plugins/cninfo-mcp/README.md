# cninfo-mcp

通过 MCP 协议从[巨潮资讯网](https://www.cninfo.com.cn)查询和下载A股上市公司年报的 Claude Code 插件。

## 功能特性

- 按股票代码查询年报列表
- 按年份筛选年报
- 下载年报 PDF 到本地目录
- 查询和下载招股说明书

## 安装方式

```
/plugin install cninfo-mcp@china-fin-toolkit
```

或通过 Marketplace 安装：

```
/plugin marketplace add youhaozhao/china-fin-toolkit
/plugin install cninfo-mcp@china-fin-toolkit
```

## 使用示例

安装完成后，即可在 Claude Code 中使用以下 MCP 工具：

### 查询年报

> 查询贵州茅台（600519）的年报

### 下载年报

> 下载贵州茅台2023年年报，保存到 ~/reports/

### 查询招股书

> 查询中科德芯（688777）的招股书

## MCP 服务

本插件通过 `npx` 运行 `@youhaozhao/cninfo-mcp`，无需额外安装依赖。

## 许可证

MIT
