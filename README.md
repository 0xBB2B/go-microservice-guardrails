# Go Microservice Guardrails

`Go Microservice Guardrails` 是一个面向 Go 微服务研发的开源 Skill 仓库，用来把一套可复用的架构规范交给 Claude Code、OpenAI Codex 和 Gemini CLI。

它适合以下场景：

- 新建 Go 微服务仓库骨架
- 整改已有微服务项目的目录边界和依赖关系
- 评审 gRPC / proto / Buf / contracts / services / pkg / ops 设计是否合理
- 统一服务边界、接口所有权、配置边界、数据最小权限、服务间鉴权、可观测性、部署与测试约束

## 仓库内容

`规范/` 目录下保存的是规则源文件，这些文件是 `go-microservice-guardrails` Skill 的生成和维护输入。

对外安装、使用和引用时，请统一以 `go-microservice-guardrails` Skill 为准，不要直接引用 `规范/` 目录下的源文件路径。

公开 Skill 位于：

- `skills/go-microservice-guardrails/SKILL.md`

## 一键安装

默认安装目标都是全局作用域。

### Claude Code

在 Claude Code 中执行下面两条命令：

```text
/plugin marketplace add 0xBB2B/go-microservice-guardrails
/plugin install go-microservice-guardrails@go-microservice-guardrails
```

安装完成后，重启 Claude Code。

Claude 官方插件文档说明了通过 marketplace 添加和安装插件的流程：
https://docs.claude.com/en/docs/claude-code/plugins

### Codex

推荐直接对 Codex 说：

```text
Fetch and follow instructions from https://raw.githubusercontent.com/0xBB2B/go-microservice-guardrails/main/.codex/INSTALL.md
```

如果你更想手动安装，可直接运行：

```bash
git clone https://github.com/0xBB2B/go-microservice-guardrails.git ~/.codex/.go-microservice-guardrails && mkdir -p ~/.agents/skills && ln -sfn ~/.codex/.go-microservice-guardrails/skills/go-microservice-guardrails ~/.agents/skills/go-microservice-guardrails
```

### Gemini CLI

Gemini CLI 支持从 GitHub 仓库直接安装扩展。执行：

```bash
gemini extensions install https://github.com/0xBB2B/go-microservice-guardrails.git --consent
```

更新时可执行：

```bash
gemini extensions update go-microservice-guardrails
```

## 安装后如何使用

安装完成后，你可以直接向 agent 提出类似请求：

- “按这套规范设计一个新的 Go 微服务仓库骨架”
- “检查这个 `services/` 和 `pkg/` 的边界是否合理”
- “按规范补齐 `contracts/`、Buf 和生成代码目录”
- “评审这套服务间鉴权和 metadata 透传设计”

Skill 会优先处理以下主题：

1. 服务边界和接口所有权
2. 共享契约真源、proto 组织与代码生成
3. 服务间通信、服务认证、方法授权和用户上下文透传
4. 服务私有配置与共享基础设施边界
5. 数据访问最小权限、部署资源组织和测试分层
6. 可观测性、缓存刷新和热更新策略

## 目录结构

```text
.
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── .codex/
│   └── INSTALL.md
├── AGENTS.md
├── gemini-extension.json
├── skills/
│   └── go-microservice-guardrails/
│       └── SKILL.md
└── 规范/
    ├── 内规-仓库模块与目录约定.md
    ├── 内规-共享契约与代码生成约定.md
    ├── 内规-服务间通信与权限验证约定.md
    ├── 内规-配置与共享包边界约定.md
    ├── 通用-服务边界与接口所有权.md
    ├── 通用-数据访问最小权限.md
    ├── 内规-数据库、部署与测试约定.md
    └── 通用-可观测性与热更新.md
```

## 更新与卸载

### Claude Code

- 在 `/plugin` 面板中更新或卸载 `go-microservice-guardrails`

### Codex

更新：

```bash
cd ~/.codex/.go-microservice-guardrails && git pull
```

卸载：

```bash
rm ~/.agents/skills/go-microservice-guardrails
```

如果你还想删除本地仓库副本：

```bash
rm -rf ~/.codex/.go-microservice-guardrails
```

### Gemini CLI

卸载：

```bash
gemini extensions uninstall go-microservice-guardrails
```

## 仓库定位

这个仓库不是业务代码模板，而是架构规范 Skill。

它不直接生成某个固定业务服务，而是把一组稳定的 Go 微服务架构约束交给 agent，使 agent 在设计、生成、整改和评审时遵循同一套边界规则。
