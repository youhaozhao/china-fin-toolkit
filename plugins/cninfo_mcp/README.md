# cninfo_mcp

A Claude Code plugin for querying and downloading annual reports of Chinese listed companies from [CNINFO](https://www.cninfo.com.cn) via the MCP protocol.

## Features

- Query annual reports by stock code
- Filter reports by year
- Download PDF reports to local directory
- Query and download prospectus documents

## Installation

```
/plugin install cninfo_mcp
```

Or install from the marketplace:

```
/plugin marketplace add youhaozhao/china-fin-toolkit
/plugin install cninfo_mcp
```

## Usage

Once installed, the following MCP tools are available in Claude Code:

### Query Annual Reports

Ask Claude to query reports for a company:

> 查询贵州茅台（600519）的年报

### Download Annual Reports

> 下载贵州茅台2023年年报，保存到 ~/reports/

### Query Prospectus

> 查询中科德芯（688777）的招股书

## MCP Server

This plugin runs `@youhaozhao/cninfo-mcp` via `npx`. No additional installation is required.

## License

MIT
