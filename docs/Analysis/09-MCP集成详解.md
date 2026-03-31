# Claude Code MCP 集成详解

## MCP 概述

Model Context Protocol (MCP) 是一个开放协议,允许 Claude Code 集成外部工具和服务。

## MCP 架构

### 1. 客户端-服务器模型

```
Claude Code (Client) ←→ MCP Server ←→ External Service
```

### 2. 传输层

支持多种传输方式:

**Stdio Transport**:
```typescript
new StdioClientTransport({
  command: 'uvx',
  args: ['mcp-server-package']
})
```

**SSE Transport**:
```typescript
new SSEClientTransport({
  url: 'https://example.com/mcp'
})
```

**WebSocket Transport**:
```typescript
new WebSocketTransport({
  url: 'wss://example.com/mcp'
})
```

## MCP 配置

### 1. 配置文件位置

- 用户级: `~/.claude/settings/mcp.json`
- 工作区级: `.claude/settings/mcp.json`

### 2. 配置格式

```json
{
  "mcpServers": {
    "github": {
      "command": "uvx",
      "args": ["mcp-server-github"],
      "env": {
        "GITHUB_TOKEN": "..."
      }
    }
  }
}
```

## MCP 功能

### 1. 工具 (Tools)

MCP 服务器可以提供工具:

```typescript
// 列出工具
const tools = await client.listTools()

// 调用工具
const result = await client.callTool({
  name: 'search_repos',
  arguments: { query: 'react' }
})
```

### 2. 资源 (Resources)

MCP 服务器可以提供资源:

```typescript
// 列出资源
const resources = await client.listResources()

// 读取资源
const content = await client.readResource({
  uri: 'github://repo/file.txt'
})
```

### 3. 提示符 (Prompts)

MCP 服务器可以提供提示符模板:

```typescript
// 列出提示符
const prompts = await client.listPrompts()

// 获取提示符
const prompt = await client.getPrompt({
  name: 'code_review',
  arguments: { file: 'src/app.ts' }
})
```

## 官方 MCP 服务器

### 1. 文件系统

```json
{
  "filesystem": {
    "command": "uvx",
    "args": ["mcp-server-filesystem", "/path/to/dir"]
  }
}
```

### 2. GitHub

```json
{
  "github": {
    "command": "uvx",
    "args": ["mcp-server-github"],
    "env": {
      "GITHUB_TOKEN": "${GITHUB_TOKEN}"
    }
  }
}
```

### 3. Google Drive

```json
{
  "google-drive": {
    "command": "uvx",
    "args": ["mcp-server-google-drive"]
  }
}
```

## MCP 工具集成

### 1. 工具转换

MCP 工具自动转换为 Claude Code 工具:

```typescript
// MCP 工具定义
{
  name: 'search_files',
  description: 'Search for files',
  inputSchema: { ... }
}

// 转换为 Claude Code 工具
MCPTool({
  server: 'filesystem',
  tool: 'search_files',
  arguments: { ... }
})
```

### 2. 权限管理

MCP 工具调用需要权限:
- 自动批准列表
- 用户确认
- 拒绝规则

## MCP 连接管理

### 1. 连接池

```typescript
const connectionPool = new Map<string, MCPServerConnection>()
```

### 2. 自动重连

连接断开时自动重连:

```typescript
client.on('disconnect', () => {
  reconnect()
})
```

### 3. 健康检查

定期检查连接状态:

```typescript
setInterval(() => {
  checkHealth()
}, 30000)
```

## MCP 安全

### 1. 沙箱隔离

MCP 服务器在隔离环境中运行。

### 2. 权限控制

- 工具调用权限
- 资源访问权限
- 环境变量隔离

### 3. 审计日志

记录所有 MCP 操作:
- 工具调用
- 资源访问
- 错误信息
