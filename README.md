# Hermes Profile Memory Bank 🏛️

每个 Hermes Agent Profile 维护结构化文件记忆 — 解决 memory 工具 2200 字配额瓶颈。

受 **Agent-Zero** (Michael Sitarzewski) 启发。

## 问题

Hermes 内置 `memory` 工具只有 2200 字配额，多 profile 共享一个池。复杂项目根本不够用。

## 方案

每个 Profile 独立维护三个文件：

```
~/.hermes/profiles/<name>/memory-bank/
├── whoami.md       # 身份、任务、规则
├── progress.md     # 做了什么、当前问题、下一步
└── learnings.md    # 模式、踩坑、纠正
```

## 安装
```bash
git clone https://github.com/remix2111/hermagent-profile-memory-bank.git
cp -r hermagent-profile-memory-bank/skills/profile-memory-bank ~/.hermes/skills/
```

## 使用
/skill profile-memory-bank

## License
MIT