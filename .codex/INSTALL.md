# Go Microservice Guardrails for Codex

## 快速安装

如果你已经在 Codex 里，可以直接说：

```text
Fetch and follow instructions from https://raw.githubusercontent.com/0xBB2B/go-microservice-guardrails/main/.codex/INSTALL.md
```

## 手动全局安装

前提：

- 已安装 `git`
- 已安装 Codex

执行：

```bash
git clone https://github.com/0xBB2B/go-microservice-guardrails.git ~/.codex/.go-microservice-guardrails
mkdir -p ~/.agents/skills
ln -sfn ~/.codex/.go-microservice-guardrails/skills/go-microservice-guardrails ~/.agents/skills/go-microservice-guardrails
```

## 如何工作

Codex 会从标准 Skill 目录中发现 Skill：

```text
~/.agents/skills/go-microservice-guardrails
```

该目录指向本仓库里的：

```text
~/.go-microservice-guardrails/skills/go-microservice-guardrails
```

安装后，重启 Codex。需要时，Codex 会读取：

- `SKILL.md`

`规范/` 目录下的文件是规则源文件，用来生成和维护 `go-microservice-guardrails` Skill。对外使用时请以 Skill 为准，不要直接引用这些源文件。

## 更新

```bash
cd ~/.codex/.go-microservice-guardrails && git pull
```

## 卸载

```bash
rm ~/.agents/skills/go-microservice-guardrails
```

如果你还想删除仓库副本：

```bash
rm -rf ~/.codex/.go-microservice-guardrails
```

## 验证

重新启动 Codex 后，可以直接提出类似请求：

- “按 Go 微服务规范设计一个新服务目录骨架”
- “检查这个 proto 和 `contracts/` 布局是否符合规范”
- “评审这套服务间鉴权和 metadata 透传是否合理”
