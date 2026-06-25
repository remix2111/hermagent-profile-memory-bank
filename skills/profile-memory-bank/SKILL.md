---
name: profile-memory-bank
description: 每个 Hermes Profile 维护结构化文件记忆 — whoami/progress/learnings 三层记忆，解决 memory 工具 2200 字配额瓶颈。受 Agent-Zero (Michael Sitarzewski) 启发。
version: 1.0.0
user-invocable: true
---

# Profile Memory Bank

每个 Profile 维护一个结构化的持久记忆目录（markdown 文件），不占用 memory 工具的 2200 字配额。

灵感来源：Agent-Zero by Michael Sitarzewski (github.com/msitarzewski)

## 触发条件

- 首次进入某个 profile 时，检查 memory-bank 是否存在
- 每次任务完成后，更新 progress.md
- 发现新模式/错误/教训时，追加 learnings.md

## 目录结构

```
~/.hermes/profiles/<name>/memory-bank/
├── whoami.md       # 身份、任务、规则（几乎不改）
├── progress.md     # 上次做了什么、当前问题、下次要做
└── learnings.md    # 发现的模式、踩过的坑、纠正的决策
```

Default profile 特殊路径：`~/.hermes/memory-bank/`

## 初始化（首次进入 profile 时）

如果 memory-bank 目录不存在或缺少文件，创建缺失的文件并填入合理内容：

```bash
mkdir -p ~/.hermes/profiles/<name>/memory-bank/
# 或 default: mkdir -p ~/.hermes/memory-bank/
```

### whoami.md 模板

```markdown
# whoami — <Profile名称>

## 身份
<这个 profile 的 Agent 是谁、做什么>

## 核心任务
- <任务1>
- <任务2>

## 规则/约束
- <硬性规则>
- <风险纪律>

## 自检机制（如有）
1. <自检项1>
2. <自检项2>
```

从系统 prompt 和 SOUL.md 中提取身份信息填入。

### progress.md 模板

```markdown
# progress — <Profile名称> 当前状态

## 上次做了什么
- YYYY-MM-DD：<做了什么>
- YYYY-MM-DD：<做了什么>

## 当前问题
1. 🔴 <严重问题>
2. 🟡 <一般问题>

## 下次要做
1. <下一步行动1>
2. <下一步行动2>

## 参考
- 项目目录：<路径>
- 关键文件：<路径>
```

### learnings.md 模板

```markdown
# learnings — <Profile名称> 经验教训

## 已发现的模式
### <模式名>
- <具体描述>
- <应对策略>

## 被纠正的错误
- <错误描述> → <正确做法>

## 工具使用坑
- <坑描述> → <解决方案>
```

## 三个文件的职责

| 文件 | 放什么 | 不放什么 |
|------|--------|----------|
| **whoami.md** | 身份定义、核心任务、数据管道、风险纪律、自检机制 | 临时任务进度、一次性发现 |
| **progress.md** | 上次做了什么、当前问题列表（带优先级）、下次要做的、参考路径 | 环境信息（VPS IP等→放memory工具） |
| **learnings.md** | 重复出现的模式、被纠正的错误、工具使用坑 | 单次故障记录 |

## 与 SOUL.md / memory 工具的区别

| | SOUL.md | memory-bank/ | memory 工具 |
|---|---|---|---|
| 内容 | 人格+行为规则 | 工作记忆+经验 | 共享事实 |
| 改动频率 | 几乎不改 | 每次任务后更新 | 发现新事实时 |
| 例子 | "你是量化交易agent" | "上次扫描命中率45%" | "VPS IP是64.188..." |
| 容量 | 不限 | 不限 | 2200字 |

## 为什么用文件不用 memory 工具

1. **容量**：memory 工具仅 2200 字，多个 profile 共用一个 blob。文件不受限
2. **结构**：memory 是扁平的键值对。文件可以分层、加章节、写表格
3. **隔离**：每个 profile 的文件互不干扰。memory 是所有 profile 共享的
4. **可审计**：`cat ~/.hermes/profiles/polymarket/memory-bank/progress.md` 一目了然

## 更新时机

- **每次任务完成**：更新 progress.md（做了什么、还有什么问题、下一步）
- **发现新模式/坑**：追加 learnings.md（只追加真正新的东西，别重复）
- **whoami.md**：几乎不改，只在角色/任务发生根本变化时更新

## 实际案例

Polymarket profile 的 learnings.md 记录：
- Open-Meteo 对欧亚内陆系统性低估 +2°C
- 概率模型 ≤1°→60% edge 太激进（实际 45%）
- ColdMath 交易员信号质量高
- 04:00 UTC 扫描 0-event bug

下次 Polymarket profile 启动时读到这些，不需要重新发现。
