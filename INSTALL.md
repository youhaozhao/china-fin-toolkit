# 安装指南 - Codex

本指南将帮助你将 China Financial Toolkit 的 MCP Servers 和 Skills 安装到你的 Codex 工具中。

## 前置要求

- 已安装 [Codex CLI](https://github.com/openai/codex)
- Node.js 18+ (用于运行 MCP Servers)

## 安装步骤

### 1. 克隆仓库（可选）

如果你想查看或修改源代码，可以克隆仓库：

```bash
git clone https://github.com/youhaozhao/china-fin-toolkit.git
cd china-fin-toolkit
```

如果只是使用 MCP Servers，可以跳过此步，直接安装 npm 包。

### 2. 安装 MCP Servers

MCP Servers 已发布为 npm 包，可以直接通过 npx 使用。

#### 配置 MCP Servers

编辑 Codex 的 MCP 配置文件 `~/.codex/mcp.json`（如果文件不存在则创建），添加以下内容：

```json
{
  "mcpServers": {
    "cninfo-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "@youhaozhao/cninfo-mcp"
      ]
    },
    "pdf2docx-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "@youhaozhao/pdf2docx-mcp"
      ]
    }
  }
}
```

#### 验证 MCP Servers

重启 Codex 并验证 MCP Servers 是否可用：

```bash
# 退出并重启 Codex
exit
codex

# 在 Codex 中运行
/mcp list
```

你应该看到 `cninfo-mcp` 和 `pdf2docx-mcp` 在列表中。

### 3. 安装 Skills

#### 复制 Skill 文件到 Codex Skills 目录

```bash
# 创建用户级别 skills 目录（如果不存在）
mkdir -p ~/.agents/skills

# 复制 annual-report-benchmark skill
cp -r skills/annual-report-benchmark ~/.agents/skills/

# 验证安装
ls -la ~/.agents/skills/
```

你应该看到 `annual-report-benchmark` 目录。

#### 重启 Codex

安装 Skills 后需要重启 Codex 才能生效：

```bash
# 退出 Codex
exit

# 重新启动 Codex
codex
```

### 4. 验证安装

在 Codex 中运行以下命令验证安装：

```bash
# 查看可用的 skills
/skills

# 测试 MCP Servers
"使用 cninfo-mcp 查询股票代码 600519 的年报信息"
```

## 项目结构说明

```
china-fin-toolkit/
├── plugins/                    # MCP Servers
│   ├── cninfo-mcp/            # 巨潮资讯 API
│   │   ├── .mcp.json          # MCP 配置
│   │   └── package.json
│   └── pdf2docx-mcp/          # PDF 转换工具
│       ├── .mcp.json          # MCP 配置
│       └── package.json
└── skills/                     # Codex Skills
    └── annual-report-benchmark/  # 年报财务对标分析
        ├── SKILL.md            # Skill 主文件
        └── references/         # 参考文档
            ├── required-fields.md
            ├── extraction-rules.md
            ├── metric-definitions.md
            └── excel-spec.md
```

## 使用示例

安装完成后，你可以在 Codex 中使用以下方式调用技能：

```bash
# 方式 1：直接描述需求
"帮我分析 600519、000858、600887 三家公司的 2023 年年报财务数据"

# 方式 2：明确指定使用技能
"使用 annual-report-benchmark 技能对比分析这几家公司：600519、000858"
```

## 依赖关系

`annual-report-benchmark` skill 依赖于以下 MCP Servers：

- **cninfo-mcp**: 用于查询和下载 A 股上市公司年报
- **pdf2docx-mcp**: 用于将 PDF 年报转换为可编辑的 DOCX 格式

确保这两个 MCP Servers 都已正确安装并配置，否则 skill 无法正常工作。

## 更新与卸载

### 更新

MCP Servers 会自动使用最新版本（npx 的 `-y` 参数会确保使用最新版本）。如果要手动更新：

```bash
# 清除 npx 缓存
npm cache clean --force

# 更新 Skills
git clone https://github.com/youhaozhao/china-fin-toolkit.git
cd china-fin-toolkit
cp -rf skills/annual-report-benchmark ~/.agents/skills/

# 重启 Codex
```

### 卸载

```bash
# 删除 Skills
rm -rf ~/.agents/skills/annual-report-benchmark

# 编辑 ~/.codex/mcp.json，删除 cninfo-mcp 和 pdf2docx-mcp 配置

# 重启 Codex
```

## 常见问题

### Q: MCP Server 启动失败？

A: 检查以下几点：
1. Node.js 版本是否 >= 18
2. `~/.codex/mcp.json` 配置是否正确（特别是 JSON 格式）
3. 网络连接是否正常（npx 需要下载包）
4. 查看 Codex 日志获取详细错误信息

### Q: Skill 无法被识别？

A: 确保：
1. Skill 文件已复制到 `~/.agents/skills/` 目录
2. SKILL.md 文件格式正确（包含 front matter metadata）
3. 已重启 Codex

### Q: 如何查看 Skill 的详细文档？

A: 在 Codex 中运行：

```bash
"查看 annual-report-benchmark skill 的详细说明"
```

### Q: npx 首次运行很慢？

A: 这是正常的，npx 首次运行需要下载包。后续运行会使用缓存的包，速度会快很多。

## 其他问题

如遇到其他问题，请：
1. 查看 [项目 README](./README.md)
2. 参考 [Codex 官方文档](https://github.com/openai/codex)

或者直接使用 Codex 解决问题，发送下面的 Prompt：
```text
我正在配置 Codex 使用 china-fin-toolkit 插件包，该项目的地址是 https://github.com/youhaozhao/china-fin-toolkit，请你搜索 Codex 如何配置 MCP Servers 和 Skill，然后把该项目 git clone 到本地后配置 Codex 使用这个 toolkit。
```
