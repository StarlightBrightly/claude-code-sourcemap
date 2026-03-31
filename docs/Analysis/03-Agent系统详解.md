# Claude Code Agent 系统详解

## Agent 系统概述

Agent 系统是 Claude Code 的核心特性之一,允许主 Agent 启动子 Agent 来处理特定任务。

## Agent 类型

### 1. 内置 Agent

**通用 Agent**:
- `general-purpose`: 通用任务处理
- `explore`: 代码库探索
- `plan`: 实现计划设计

**专用 Agent**:
- `statusline-setup`: 状态栏配置
- `claude-code-guide`: Claude Code 帮助
- `test-runner`: 测试运行
- `build-validator`: 构建验证

### 2. 自定义 Agent

用户可以在 `.claude/agents/` 目录定义自定义 Agent:

```markdown
---
name: my-agent
description: Custom agent description
model: opus
tools: [Bash, FileRead, FileEdit]
---

System prompt for the agent...
```

## Agent 执行模式

### 1. 前台执行 (默认)

```typescript
Agent({
  description: "Fix bug",
  prompt: "Fix the authentication bug"
})
```

- 阻塞主 Agent
- 实时显示进度
- 结果立即返回

### 2. 后台执行

```typescript
Agent({
  description: "Run tests",
  prompt: "Run all tests",
  run_in_background: true
})
```

- 不阻塞主 Agent
- 异步执行
- 完成时通知

### 3. 自动后台化

长时间运行的 Agent 会自动后台化:

```typescript
const AUTO_BACKGROUND_MS = 120_000  // 2分钟
```

## Agent 隔离模式

### 1. Worktree 隔离

创建 Git worktree 进行隔离:

```typescript
Agent({
  description: "Experimental feature",
  prompt: "Implement feature X",
  isolation: "worktree"
})
```

**特点**:
- 独立的工作目录
- 不影响主分支
- 可以保留或删除更改

### 2. Remote 隔离 (内部)

在远程环境执行:

```typescript
Agent({
  isolation: "remote"
})
```

## Agent 生命周期

### 1. 初始化阶段

```
创建 Agent ID → 设置上下文 → 加载工具 → 构建系统提示
```

### 2. 执行阶段

```
发送初始消息 → 工具调用循环 → 进度跟踪 → 结果收集
```

### 3. 清理阶段

```
保存转录 → 清理资源 → 返回结果 → 通知完成
```

## Agent 通信

### 1. SendMessage 工具

Agent 之间可以通过 SendMessage 通信:

```typescript
SendMessage({
  to: "agent-name",
  message: "Status update"
})
```

### 2. 团队模式

创建 Agent 团队:

```typescript
TeamCreate({
  name: "dev-team",
  members: ["agent1", "agent2"]
})
```

## Agent 上下文管理

### 1. 上下文继承

子 Agent 继承父 Agent 的:
- 工作目录
- 环境变量
- MCP 连接
- 权限设置

### 2. 上下文隔离

子 Agent 拥有独立的:
- 消息历史
- 文件状态缓存
- 工具调用记录

### 3. 上下文大小限制

```typescript
const READ_FILE_STATE_CACHE_SIZE = 50  // 文件状态缓存
```

## Agent 工具过滤

### 1. 工具白名单

Agent 定义可以指定允许的工具:

```yaml
tools: [Bash, FileRead, FileEdit, Grep, Glob]
```

### 2. 工具黑名单

某些工具对 Agent 不可用:

```typescript
const AGENT_DISALLOWED_TOOLS = [
  'Agent',           // 防止递归
  'EnterPlanMode',
  'ExitPlanMode'
]
```

## Agent 进度跟踪

### 1. 进度更新

```typescript
interface AgentProgress {
  status: 'running' | 'completed' | 'failed'
  tokensUsed: number
  toolCalls: number
  activityDescription: string
}
```

### 2. 活动描述

自动生成活动描述:
- 最近的工具调用
- 当前任务状态
- 进度百分比

## Agent MCP 集成

### 1. Agent 专属 MCP 服务器

Agent 可以定义自己的 MCP 服务器:

```yaml
---
mcpServers:
  custom-server:
    command: uvx
    args: [my-mcp-server]
---
```

### 2. MCP 工具继承

子 Agent 继承父 Agent 的 MCP 工具,并可添加自己的。

## 性能优化

### 1. 并行执行

多个独立 Agent 可以并行运行:

```typescript
// 并行启动多个 Agent
Agent({ description: "Task 1", prompt: "..." })
Agent({ description: "Task 2", prompt: "..." })
```

### 2. 资源管理

- 自动清理完成的 Agent
- 限制并发 Agent 数量
- 内存使用监控

### 3. 缓存策略

- 文件状态缓存
- 工具结果缓存
- 系统提示缓存
