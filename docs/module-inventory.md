# 模块清单与统计附录

## 1. 统计口径

本附录主要统计 `restored-src/src` 下的代码文件，统计时间为 `2026-03-31`。

统计口径说明：

- 代码文件类型包括 `.ts`、`.tsx`、`.js`、`.jsx`、`.mjs`、`.cjs`
- 不包含 `.git`、IDE 配置与文档目录
- 该附录偏向“查目录、查规模、查热点”，与总报告互补

## 2. 顶层目录全量统计

| 目录 | 文件数 | `.ts` | `.tsx` |
| --- | ---: | ---: | ---: |
| `utils` | 564 | 549 | 15 |
| `components` | 389 | 43 | 346 |
| `commands` | 207 | 110 | 79 |
| `tools` | 184 | 149 | 35 |
| `services` | 130 | 127 | 3 |
| `hooks` | 104 | 76 | 28 |
| `ink` | 96 | 79 | 17 |
| `bridge` | 31 | 31 | 0 |
| `constants` | 21 | 21 | 0 |
| `skills` | 20 | 20 | 0 |
| `cli` | 19 | 17 | 2 |
| `keybindings` | 14 | 12 | 2 |
| `tasks` | 12 | 8 | 4 |
| `migrations` | 11 | 11 | 0 |
| `types` | 11 | 11 | 0 |
| `context` | 9 | 0 | 9 |
| `entrypoints` | 8 | 7 | 1 |
| `memdir` | 8 | 8 | 0 |
| `buddy` | 6 | 4 | 2 |
| `state` | 6 | 5 | 1 |
| `vim` | 5 | 5 | 0 |
| `native-ts` | 4 | 4 | 0 |
| `query` | 4 | 4 | 0 |
| `remote` | 4 | 4 | 0 |
| `screens` | 3 | 0 | 3 |
| `server` | 3 | 3 | 0 |
| `plugins` | 2 | 2 | 0 |
| `upstreamproxy` | 2 | 2 | 0 |

## 3. 顶层目录代码行数统计

| 目录 | 文件数 | 代码总行数 |
| --- | ---: | ---: |
| `utils` | 564 | 181036 |
| `components` | 389 | 81935 |
| `services` | 130 | 53810 |
| `tools` | 184 | 51012 |
| `commands` | 207 | 26656 |
| `ink` | 96 | 19938 |
| `hooks` | 104 | 19308 |
| `bridge` | 31 | 12644 |
| `cli` | 19 | 12372 |
| `screens` | 3 | 5980 |
| `main.tsx` | 1 | 4684 |
| `skills` | 20 | 4086 |
| `native-ts` | 4 | 4085 |
| `entrypoints` | 8 | 4059 |
| `types` | 11 | 3457 |

从这一组数据可以看出：

- `commands` 文件很多，但单文件平均较小。
- `services`、`tools`、`utils` 文件数量和总行数都很高，是系统复杂度主战场。
- `screens` 只有 3 个文件却接近 6000 行，说明交互主界面极重。

## 4. 命令目录清单

### 4.1 `commands/` 子目录

以下为 `restored-src/src/commands` 下的一级子目录：

- `add-dir`
- `agents`
- `ant-trace`
- `autofix-pr`
- `backfill-sessions`
- `branch`
- `break-cache`
- `bridge`
- `btw`
- `bughunter`
- `chrome`
- `clear`
- `color`
- `compact`
- `config`
- `context`
- `copy`
- `cost`
- `ctx_viz`
- `debug-tool-call`
- `desktop`
- `diff`
- `doctor`
- `effort`
- `env`
- `exit`
- `export`
- `extra-usage`
- `fast`
- `feedback`
- `files`
- `good-claude`
- `heapdump`
- `help`
- `hooks`
- `ide`
- `install-github-app`
- `install-slack-app`
- `issue`
- `keybindings`
- `login`
- `logout`
- `mcp`
- `memory`
- `mobile`
- `mock-limits`
- `model`
- `oauth-refresh`
- `onboarding`
- `output-style`
- `passes`
- `perf-issue`
- `permissions`
- `plan`
- `plugin`
- `pr_comments`
- `privacy-settings`
- `rate-limit-options`
- `release-notes`
- `reload-plugins`
- `remote-env`
- `remote-setup`
- `rename`
- `reset-limits`
- `resume`
- `review`
- `rewind`
- `sandbox-toggle`
- `session`
- `share`
- `skills`
- `stats`
- `status`
- `stickers`
- `summary`
- `tag`
- `tasks`
- `teleport`
- `terminalSetup`
- `theme`
- `thinkback`
- `thinkback-play`
- `upgrade`
- `usage`
- `vim`
- `voice`

### 4.2 `commands/` 根文件

除了子目录，还存在一批核心入口文件：

- `advisor.ts`
- `bridge-kick.ts`
- `brief.ts`
- `commit-push-pr.ts`
- `commit.ts`
- `createMovedToPluginCommand.ts`
- `init-verifiers.ts`
- `init.ts`
- `insights.ts`
- `install.tsx`
- `review.ts`
- `security-review.ts`
- `statusline.tsx`
- `ultraplan.tsx`
- `version.ts`

这些根文件通常承担“高层入口命令”“共享命令壳层”“历史兼容命令”或“重量级功能命令”的角色。

## 5. 工具目录清单

`restored-src/src/tools` 下的一级工具目录如下：

- `AgentTool`
- `AskUserQuestionTool`
- `BashTool`
- `BriefTool`
- `ConfigTool`
- `EnterPlanModeTool`
- `EnterWorktreeTool`
- `ExitPlanModeTool`
- `ExitWorktreeTool`
- `FileEditTool`
- `FileReadTool`
- `FileWriteTool`
- `GlobTool`
- `GrepTool`
- `LSPTool`
- `ListMcpResourcesTool`
- `MCPTool`
- `McpAuthTool`
- `NotebookEditTool`
- `PowerShellTool`
- `REPLTool`
- `ReadMcpResourceTool`
- `RemoteTriggerTool`
- `ScheduleCronTool`
- `SendMessageTool`
- `SkillTool`
- `SleepTool`
- `SyntheticOutputTool`
- `TaskCreateTool`
- `TaskGetTool`
- `TaskListTool`
- `TaskOutputTool`
- `TaskStopTool`
- `TaskUpdateTool`
- `TeamCreateTool`
- `TeamDeleteTool`
- `TodoWriteTool`
- `ToolSearchTool`
- `WebFetchTool`
- `WebSearchTool`
- `shared`
- `testing`

`tools/` 根目录几乎没有单独逻辑文件，只有一个 `utils.ts`，这说明工具实现以“目录即模块”的方式组织得比较完整。

### 5.1 `tools/` 中规模最大的子模块

| 子模块 | 文件数 |
| --- | ---: |
| `AgentTool` | 20 |
| `BashTool` | 18 |
| `PowerShellTool` | 14 |
| `FileEditTool` | 6 |
| `LSPTool` | 6 |
| `BriefTool` | 5 |
| `ConfigTool` | 5 |
| `FileReadTool` | 5 |
| `ScheduleCronTool` | 5 |
| `WebFetchTool` | 5 |

这说明工具层最复杂的三块不是文件编辑本身，而是：

- 子 Agent 管理
- Shell 执行
- PowerShell 安全与路径校验

## 6. 服务目录清单

`restored-src/src/services` 下的一级子目录如下：

- `AgentSummary`
- `MagicDocs`
- `PromptSuggestion`
- `SessionMemory`
- `analytics`
- `api`
- `autoDream`
- `compact`
- `extractMemories`
- `lsp`
- `mcp`
- `oauth`
- `plugins`
- `policyLimits`
- `remoteManagedSettings`
- `settingsSync`
- `teamMemorySync`
- `tips`
- `toolUseSummary`
- `tools`

### 6.1 `services/` 根文件

- `awaySummary.ts`
- `claudeAiLimits.ts`
- `claudeAiLimitsHook.ts`
- `diagnosticTracking.ts`
- `internalLogging.ts`
- `mcpServerApproval.tsx`
- `mockRateLimits.ts`
- `notifier.ts`
- `preventSleep.ts`
- `rateLimitMessages.ts`
- `rateLimitMocking.ts`
- `tokenEstimation.ts`
- `vcr.ts`
- `voice.ts`
- `voiceKeyterms.ts`
- `voiceStreamSTT.ts`

### 6.2 `services/` 中规模最大的子模块

| 子模块 | 文件数 |
| --- | ---: |
| `mcp` | 23 |
| `api` | 20 |
| `compact` | 11 |
| `analytics` | 9 |
| `lsp` | 7 |
| `oauth` | 5 |
| `remoteManagedSettings` | 5 |
| `teamMemorySync` | 5 |

这几乎可以直接当作项目最核心的后端能力层划分：

- API 层
- MCP 层
- 上下文压缩层
- 分析/埋点层
- 编辑器与远程设置层

## 7. 组件层清单摘要

`components/` 是纯前端意义上的“终端界面层”，其规模最大的子目录如下：

| 子目录 | 文件数 |
| --- | ---: |
| 根目录文件 | 113 |
| `permissions` | 51 |
| `messages` | 41 |
| `agents` | 26 |
| `PromptInput` | 21 |
| `design-system` | 16 |
| `LogoV2` | 15 |
| `mcp` | 13 |
| `Spinner` | 12 |
| `tasks` | 12 |
| `CustomSelect` | 10 |
| `FeedbackSurvey` | 9 |

可以据此得出几个判断：

- 权限请求 UI 是一整套独立设计，不是零散弹窗。
- 消息呈现与输入框系统都很复杂。
- Agent、MCP、任务管理都有专门界面。
- 这个“CLI”实际上拥有完整的终端应用前端。

## 8. 工具基础设施层摘要

`utils/` 的顶层文件极多，说明项目把大量关键逻辑放在非 UI、非 service 的基础设施层中。

规模最大的 `utils/` 子目录如下：

| 子目录 | 文件数 |
| --- | ---: |
| 根目录文件 | 298 |
| `plugins` | 44 |
| `permissions` | 24 |
| `bash` | 23 |
| `swarm` | 22 |
| `settings` | 19 |
| `hooks` | 17 |
| `model` | 16 |
| `computerUse` | 15 |
| `shell` | 10 |
| `telemetry` | 9 |

根目录文件里最能代表项目骨架的一批模块包括：

- `messages.ts`
- `sessionStorage.ts`
- `auth.ts`
- `config.ts`
- `queryContext.ts`
- `queryHelpers.ts`
- `forkedAgent.ts`
- `fileHistory.ts`
- `git.ts`
- `permissions/*`
- `plugins/*`
- `mcpOutputStorage.ts`
- `toolResultStorage.ts`
- `sideQuestion.ts`
- `sessionRestore.ts`

这说明项目基础设施不是散落在 `services/` 里，而是高度下沉到了 `utils/`。

## 9. 最大文件清单

按行数排序，当前仓库最重的 20 个文件如下：

| 排名 | 文件 | 行数 |
| --- | --- | ---: |
| 1 | `restored-src/src/cli/print.ts` | 5595 |
| 2 | `restored-src/src/utils/messages.ts` | 5513 |
| 3 | `restored-src/src/utils/sessionStorage.ts` | 5106 |
| 4 | `restored-src/src/utils/hooks.ts` | 5023 |
| 5 | `restored-src/src/screens/REPL.tsx` | 5006 |
| 6 | `restored-src/src/main.tsx` | 4684 |
| 7 | `restored-src/src/utils/bash/bashParser.ts` | 4437 |
| 8 | `restored-src/src/utils/attachments.ts` | 3998 |
| 9 | `restored-src/src/services/api/claude.ts` | 3420 |
| 10 | `restored-src/src/services/mcp/client.ts` | 3349 |
| 11 | `restored-src/src/utils/plugins/pluginLoader.ts` | 3303 |
| 12 | `restored-src/src/commands/insights.ts` | 3201 |
| 13 | `restored-src/src/bridge/bridgeMain.ts` | 3000 |
| 14 | `restored-src/src/utils/bash/ast.ts` | 2680 |
| 15 | `restored-src/src/utils/plugins/marketplaceManager.ts` | 2644 |
| 16 | `restored-src/src/tools/BashTool/bashPermissions.ts` | 2622 |
| 17 | `restored-src/src/tools/BashTool/bashSecurity.ts` | 2593 |
| 18 | `restored-src/src/native-ts/yoga-layout/index.ts` | 2579 |
| 19 | `restored-src/src/services/mcp/auth.ts` | 2466 |
| 20 | `restored-src/src/bridge/replBridge.ts` | 2407 |

从这份清单可以看出，复杂度热点集中在：

- CLI/SDK 输出驱动
- 消息规范化
- 会话持久化
- Hook 体系
- 交互主屏
- Shell 解析与安全
- MCP 客户端
- 插件系统
- Bridge/Remote 能力

## 10. 外部依赖线索

由于当前仓库不包含完整依赖声明，这里用源码导入统计反推第三方技术栈。出现频次较高的外部依赖包括：

| 依赖 | 导入次数 | 说明 |
| --- | ---: | --- |
| `react` | 756 | UI 核心 |
| `react/compiler-runtime` | 395 | React 编译器运行时痕迹 |
| `bun:bundle` | 196 | Bun 构建特性宏 |
| `zod/v4` | 125 | schema 与输入校验 |
| `axios` | 57 | HTTP 调用 |
| `@anthropic-ai/sdk/resources/index.mjs` | 53 | Anthropic 消息结构 |
| `@anthropic-ai/sdk` | 24 | 模型 API SDK |
| `@anthropic-ai/sdk/resources/beta/messages/messages.mjs` | 22 | beta 消息接口 |
| `@modelcontextprotocol/sdk/types.js` | 20 | MCP 类型系统 |
| `diff` | 19 | diff/patch 类功能 |
| `execa` | 16 | 子进程执行 |
| `usehooks-ts` | 14 | 通用 Hook |
| `@opentelemetry/api` | 10 | 遥测 |
| `undici` | 6 | 网络层 |
| `qrcode` | 5 | 二维码 |
| `marked` | 5 | Markdown 处理 |
| `ignore` | 5 | ignore 规则处理 |
| `semver` | 5 | 版本比较 |

这个统计的意义不在于精确还原 `package.json`，而在于帮助理解项目确实横跨了：

- 终端 UI
- 模型 API
- MCP
- 网络请求
- schema 校验
- 遥测
- Shell/进程
- Markdown/内容处理

## 11. 包内置二进制线索

`package/vendor` 中可以确认存在以下内置二进制或原生扩展：

### 11.1 `ripgrep`

- `arm64-darwin`
- `arm64-linux`
- `arm64-win32`
- `x64-darwin`
- `x64-linux`
- `x64-win32`

### 11.2 `audio-capture`

- `arm64-darwin`
- `arm64-linux`
- `arm64-win32`
- `x64-darwin`
- `x64-linux`
- `x64-win32`

这说明发布包为了跨平台一致性，已经把关键搜索和音频能力做成 vendored 资产随包分发。

## 12. 入口与协议文件

`entrypoints/` 下可确认存在以下入口或协议文件：

- `agentSdkTypes.ts`
- `cli.tsx`
- `init.ts`
- `mcp.ts`
- `sandboxTypes.ts`
- `sdk/controlSchemas.ts`
- `sdk/coreSchemas.ts`
- `sdk/coreTypes.ts`

从这些命名就能看出项目至少维护三套入口面：

- 交互式 CLI
- SDK/结构化协议
- MCP 与沙箱相关类型边界

## 13. 测试资产现状

在当前仓库中没有发现：

- 标准 `test`/`tests`/`__tests__` 目录
- 常规 `*.test.*` 文件
- 常规 `*.spec.*` 文件

几乎唯一被 `test` 命名模式命中的只是 `restored-src/src/ink/hit-test.ts`，它显然不是单元测试目录意义上的测试文件。

结论很明确：这个仓库适合做源码阅读与架构分析，不适合作为“保留完整测试上下文”的开发仓库来使用。

## 14. 适合继续深挖的专题

如果后续还要继续分析，最值得单独拆专题的方向有：

1. `messages.ts` 与 `sessionStorage.ts`：消息协议和长会话设计
2. `QueryEngine.ts` / `query.ts` / `services/api/claude.ts`：代理执行内核
3. `services/mcp/client.ts`：MCP 接入模型
4. `tools/AgentTool` 与 `coordinator/`：多 Agent 机制
5. `utils/sandbox` 与 `tools/BashTool`：权限、安全和命令执行
6. `utils/plugins` / `skills`：扩展系统
7. `components/permissions` / `components/messages` / `screens/REPL.tsx`：终端应用前端

这几个专题基本覆盖了整个系统的复杂度中心。
