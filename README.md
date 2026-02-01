# go-zero AI Context

English | [简体中文](#简体中文)

Transform any AI coding assistant into a go-zero expert with one prompt.

## One-Prompt Setup

Just tell your AI assistant:

```
Set up go-zero AI tools for this project from https://github.com/zeromicro/ai-context
```

Your AI will automatically:
1. Detect which AI tool you're using (Claude Code, Cursor, Copilot, Windsurf)
2. Install the appropriate configuration
3. Set up zero-skills knowledge base
4. Configure mcp-zero tools (if using Claude)

## What Gets Installed

This prompt sets up a three-layer AI assistance system:

```
┌─────────────────────────────────────────────────────────────┐
│                     AI Assistant                            │
│  (Claude Code, GitHub Copilot, Cursor, Windsurf)           │
└────────────┬─────────────────────┬──────────────────────────┘
             │                     │
             ├─ Workflow Layer ────┤
             │  ai-context         │  "What to do" - Quick decisions
             │  (~5KB)             │  Loaded for every interaction
             │                     │
             ├─ Knowledge Layer ───┤
             │  zero-skills        │  "How & Why" - Detailed patterns
             │  (~40KB)            │  Loaded when needed
             │                     │
             └─ Execution Layer ───┘
                mcp-zero             "Do it" - Run goctl commands
                (MCP Server)          Generate actual code files
```

| Component | Purpose | Size | Repository |
|-----------|---------|------|------------|
| **ai-context** | Workflow instructions, decision trees | ~5KB | [zeromicro/ai-context](https://github.com/zeromicro/ai-context) |
| **zero-skills** | Comprehensive patterns, best practices | ~40KB | [zeromicro/zero-skills](https://github.com/zeromicro/zero-skills) |
| **mcp-zero** | Runtime tools, code generation | MCP Server | [zeromicro/mcp-zero](https://github.com/zeromicro/mcp-zero) |

## Manual Setup

If you prefer manual installation, choose your AI tool:

### Claude Code (Recommended)

```bash
# Install ai-context (workflow instructions)
git clone https://github.com/zeromicro/ai-context.git .claude/ai-context

# Install zero-skills (knowledge base)
git clone https://github.com/zeromicro/zero-skills.git .claude/skills/zero-skills

# Install mcp-zero (code generation tools)
git clone https://github.com/zeromicro/mcp-zero.git ~/.mcp-zero
cd ~/.mcp-zero && go build -o mcp-zero main.go

# Configure mcp-zero in Claude Code
claude mcp add mcp-zero --transport stdio \
  --env GOCTL_PATH=$(which goctl) \
  -- ~/.mcp-zero/mcp-zero
```

### GitHub Copilot

```bash
# Add ai-context as submodule
git submodule add https://github.com/zeromicro/ai-context.git .github/ai-context

# Create symlink for Copilot
ln -s ai-context/00-instructions.md .github/copilot-instructions.md

# Add zero-skills for reference
git clone https://github.com/zeromicro/zero-skills.git .ai-context/zero-skills
```

### Cursor

```bash
# Add ai-context as rules directory
git submodule add https://github.com/zeromicro/ai-context.git .cursorrules

# Add zero-skills for reference
git clone https://github.com/zeromicro/zero-skills.git .ai-context/zero-skills
```

Cursor automatically reads all `.md` files in `.cursorrules` directory.

### Windsurf

```bash
# Add ai-context as rules directory
git submodule add https://github.com/zeromicro/ai-context.git .windsurfrules

# Add zero-skills for reference
git clone https://github.com/zeromicro/zero-skills.git .ai-context/zero-skills
```

## After Setup

Once installed, your AI assistant can:

**Generate Services:**
```
Create a user management API with CRUD operations
```

**Apply Patterns:**
```
Add rate limiting and circuit breaker to my API
```

**Troubleshoot Issues:**
```
Why am I getting "http: named cookie not present" error?
```

**Follow Best Practices:**
```
Review my handler code for go-zero anti-patterns
```

## Updating

Keep your AI context up to date:

```bash
# Update ai-context
git submodule update --remote .github/ai-context  # Copilot
git submodule update --remote .cursorrules        # Cursor
git submodule update --remote .windsurfrules      # Windsurf

# Update zero-skills
cd .claude/skills/zero-skills && git pull         # Claude Code
cd .ai-context/zero-skills && git pull            # Others
```

## How It Works

### ai-context (This Repo)

Provides lightweight workflow instructions:
- **Decision trees**: When to use API vs RPC
- **File priority**: Which files to read first
- **Tool usage**: How to use goctl commands
- **Quick patterns**: Common code snippets

### zero-skills

Provides comprehensive knowledge:
- **REST API patterns**: Handler → Logic → Model architecture
- **RPC patterns**: Service discovery, load balancing
- **Database patterns**: SQL, MongoDB, Redis, caching
- **Resilience patterns**: Circuit breaker, rate limiting
- **Troubleshooting**: Common errors and solutions

### mcp-zero

Provides runtime tools:
- `create_api_service`: Generate REST API from .api file
- `create_rpc_service`: Generate gRPC service from .proto file
- `generate_model`: Generate database models
- `analyze_project`: Understand existing go-zero structure
- `query_docs`: Search go-zero documentation

## Feature Comparison

| Feature | Claude Code | Cursor | Copilot | Windsurf |
|---------|-------------|--------|---------|----------|
| ai-context | ✅ Auto-load | ✅ Via rules | ✅ Via instructions | ✅ Via rules |
| zero-skills | ✅ Native skills | ✅ Reference | ✅ Reference | ✅ Reference |
| mcp-zero | ✅ Full integration | ❌ | ❌ | ❌ |
| Code generation | ✅ Automatic | ❌ Manual goctl | ❌ Manual goctl | ❌ Manual goctl |
| Subagent workflows | ✅ | ❌ | ❌ | ❌ |

## Requirements

- Go 1.19+
- goctl (install: `go install github.com/zeromicro/go-zero/tools/goctl@latest`)
- Git

## Related Projects

- [go-zero](https://github.com/zeromicro/go-zero) - The framework
- [zero-skills](https://github.com/zeromicro/zero-skills) - Knowledge base
- [mcp-zero](https://github.com/zeromicro/mcp-zero) - MCP tools

## License

MIT License - Same as go-zero framework

---

# 简体中文

将任何 AI 编程助手变成 go-zero 专家，只需一个提示。

## 一键安装

只需告诉你的 AI 助手：

```
Set up go-zero AI tools for this project from https://github.com/zeromicro/ai-context
```

AI 会自动：
1. 检测你使用的 AI 工具（Claude Code、Cursor、Copilot、Windsurf）
2. 安装相应的配置
3. 设置 zero-skills 知识库
4. 配置 mcp-zero 工具（如果使用 Claude）

## 安装内容

这个提示会设置一个三层 AI 辅助系统：

```
┌─────────────────────────────────────────────────────────────┐
│                     AI 助手                                  │
│  (Claude Code, GitHub Copilot, Cursor, Windsurf)           │
└────────────┬─────────────────────┬──────────────────────────┘
             │                     │
             ├─ 工作流层 ──────────┤
             │  ai-context         │  "做什么" - 快速决策
             │  (~5KB)             │  每次交互都加载
             │                     │
             ├─ 知识层 ────────────┤
             │  zero-skills        │  "如何和为什么" - 详细模式
             │  (~40KB)            │  需要时加载
             │                     │
             └─ 执行层 ────────────┘
                mcp-zero             "执行" - 运行 goctl 命令
                (MCP Server)          生成实际代码文件
```

| 组件 | 用途 | 大小 | 仓库 |
|------|------|------|------|
| **ai-context** | 工作流指令、决策树 | ~5KB | [zeromicro/ai-context](https://github.com/zeromicro/ai-context) |
| **zero-skills** | 完整模式、最佳实践 | ~40KB | [zeromicro/zero-skills](https://github.com/zeromicro/zero-skills) |
| **mcp-zero** | 运行时工具、代码生成 | MCP Server | [zeromicro/mcp-zero](https://github.com/zeromicro/mcp-zero) |

## 手动安装

如果你喜欢手动安装，选择你的 AI 工具：

### Claude Code（推荐）

```bash
# 安装 ai-context（工作流指令）
git clone https://github.com/zeromicro/ai-context.git .claude/ai-context

# 安装 zero-skills（知识库）
git clone https://github.com/zeromicro/zero-skills.git .claude/skills/zero-skills

# 安装 mcp-zero（代码生成工具）
git clone https://github.com/zeromicro/mcp-zero.git ~/.mcp-zero
cd ~/.mcp-zero && go build -o mcp-zero main.go

# 在 Claude Code 中配置 mcp-zero
claude mcp add mcp-zero --transport stdio \
  --env GOCTL_PATH=$(which goctl) \
  -- ~/.mcp-zero/mcp-zero
```

### GitHub Copilot

```bash
# 添加 ai-context 作为子模块
git submodule add https://github.com/zeromicro/ai-context.git .github/ai-context

# 创建 Copilot 符号链接
ln -s ai-context/00-instructions.md .github/copilot-instructions.md

# 添加 zero-skills 作为参考
git clone https://github.com/zeromicro/zero-skills.git .ai-context/zero-skills
```

### Cursor

```bash
# 添加 ai-context 作为规则目录
git submodule add https://github.com/zeromicro/ai-context.git .cursorrules

# 添加 zero-skills 作为参考
git clone https://github.com/zeromicro/zero-skills.git .ai-context/zero-skills
```

Cursor 自动读取 `.cursorrules` 目录中的所有 `.md` 文件。

### Windsurf

```bash
# 添加 ai-context 作为规则目录
git submodule add https://github.com/zeromicro/ai-context.git .windsurfrules

# 添加 zero-skills 作为参考
git clone https://github.com/zeromicro/zero-skills.git .ai-context/zero-skills
```

## 安装后

安装完成后，你的 AI 助手可以：

**生成服务：**
```
创建一个包含 CRUD 操作的用户管理 API
```

**应用模式：**
```
给我的 API 添加限流和熔断
```

**排查问题：**
```
为什么我会收到 "http: named cookie not present" 错误？
```

**遵循最佳实践：**
```
检查我的 handler 代码是否存在 go-zero 反模式
```

## 更新

保持 AI 上下文最新：

```bash
# 更新 ai-context
git submodule update --remote .github/ai-context  # Copilot
git submodule update --remote .cursorrules        # Cursor
git submodule update --remote .windsurfrules      # Windsurf

# 更新 zero-skills
cd .claude/skills/zero-skills && git pull         # Claude Code
cd .ai-context/zero-skills && git pull            # 其他工具
```

## 工作原理

### ai-context（本仓库）

提供轻量级工作流指令：
- **决策树**：何时使用 API vs RPC
- **文件优先级**：优先读取哪些文件
- **工具使用**：如何使用 goctl 命令
- **快速模式**：常用代码片段

### zero-skills

提供完整知识：
- **REST API 模式**：Handler → Logic → Model 架构
- **RPC 模式**：服务发现、负载均衡
- **数据库模式**：SQL、MongoDB、Redis、缓存
- **弹性模式**：熔断器、限流
- **故障排查**：常见错误和解决方案

### mcp-zero

提供运行时工具：
- `create_api_service`：从 .api 文件生成 REST API
- `create_rpc_service`：从 .proto 文件生成 gRPC 服务
- `generate_model`：生成数据库模型
- `analyze_project`：理解现有 go-zero 结构
- `query_docs`：搜索 go-zero 文档

## 功能对比

| 功能 | Claude Code | Cursor | Copilot | Windsurf |
|------|-------------|--------|---------|----------|
| ai-context | ✅ 自动加载 | ✅ 通过规则 | ✅ 通过指令 | ✅ 通过规则 |
| zero-skills | ✅ 原生技能 | ✅ 引用 | ✅ 引用 | ✅ 引用 |
| mcp-zero | ✅ 完整集成 | ❌ | ❌ | ❌ |
| 代码生成 | ✅ 自动 | ❌ 手动 goctl | ❌ 手动 goctl | ❌ 手动 goctl |
| 子代理工作流 | ✅ | ❌ | ❌ | ❌ |

## 环境要求

- Go 1.19+
- goctl（安装：`go install github.com/zeromicro/go-zero/tools/goctl@latest`）
- Git

## 相关项目

- [go-zero](https://github.com/zeromicro/go-zero) - 框架本身
- [zero-skills](https://github.com/zeromicro/zero-skills) - 知识库
- [mcp-zero](https://github.com/zeromicro/mcp-zero) - MCP 工具

## 许可证

MIT License - 与 go-zero 框架相同
