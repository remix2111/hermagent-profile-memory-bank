# Hermes Profile Memory Bank 🏛️

每个 Hermes Agent Profile 维护结构化文件记忆 — 解决 memory 工具 2200 字配额瓶颈。

受 **Agent-Zero** (Michael Sitarzewski / [agency-agents](https://github.com/msitarzewski/agency-agents)) 启发。

## 问题

Hermes 内置的 `memory` 工具有 2200 字配额限制，多个 profile 共用一个记忆池。对于复杂项目（Polymarket 量化交易、SEO 自动化、IG→快手流水线），根本不够用。

## 方案

每个 Profile 独立维护三个 markdown 文件：

```
~/.hermes/profiles/<name>/memory-bank/
├── whoami.md       # 身份定义、核心任务、规则
├── progress.md     # 上次做了什么、当前问题、下一步
└── learnings.md    # 发现的模式、踩过的坑、纠正的决策
```

## 和 memory 工具的区别

| | SOUL.md | memory-bank/ | memory 工具 |
|---|---|---|---|
| 内容 | 人格+行为规则 | 工作记忆+经验 | 共享事实 |
| 容量 | 不限 | 不限 | 2200字 |
| 隔离 | Profile 独立 | Profile 独立 | 共享 |

## 安装

```bash
# 方式一：直接复制
mkdir -p ~/.hermes/skills/profile-memory-bank/
cp skills/profile-memory-bank/SKILL.md ~/.hermes/skills/profile-memory-bank/
```

```
# 方式二：Hermes skills hub
hermes skills install profile-memory-bank
```

## 使用

在任意 Hermes Profile 中加载技能：

```
/skill profile-memory-bank
```

Agent 会自动检查并初始化 memory-bank 目录。

## 实际效果

Polymarket 天气交易 Agent 的 learnings.md 记录：
- Open-Meteo 对欧亚内陆系统性低估 +2°C
- 概率模型 ≤1°→60% edge 太激进（实际 45%）
- ColdMath 交易员信号质量高

下次启动时自动读取，无需重新发现。

## License

MIT — 见 [LICENSE](LICENSE)
