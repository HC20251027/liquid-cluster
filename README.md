# Penta Harness

> 液态集群 Harness 系统 —— 让子 Agent 从"用完即弃"进化为"自然生长的集群成员"

Penta Harness 是一套 **Agent 工程规则体系**，核心思想是：**子 Agent 不是一次性工具，而是可以通过使用频率自然"转正"的集群成员。**

## 如何使用

**把本文件（README.md）复制到你的项目根目录，重命名为 `AGENTS.md`。**

AI 编程助手（Claude Code / Codex / Cursor / Windsurf 等）会自动读取 `AGENTS.md` 作为行为指南。之后每次使用 Agent 时，它会自觉遵守本文件中定义的规则——子 Agent 自然存活、白盒归档、知识库自维护、Skill 自动进化。

```bash
# 一行命令，即刻生效
curl -o AGENTS.md https://raw.githubusercontent.com/HC20251027/liquid-cluster/main/README.md
```

或者手动将本文件复制为 `AGENTS.md` 放到项目根目录即可。

---

## 你将获得的能力

任何 AI Agent 框架拉取本项目后即可获得：

- 🧬 **子 Agent 自然存活** — 高频使用的子 Agent 自动升级为常驻成员
- 📖 **Git Wiki 知识库** — AI 自维护的 Markdown 知识库，Git + YOYO 版本控制，人类随时审查
- 🧠 **四层记忆系统** — 长期记忆（共享）+ 专业记忆（独享）+ 执行日志 + 索引目录
- 📋 **白盒归档** — 每次子 Agent 执行的完整轨迹被持久化保存
- 🔄 **GEPA 进化** — 归档数据 → 模式提取 → Skill 优化建议，所有框架通用
- 🌊 **液态拓扑** — 父 Agent 充当 IM 路由器，实现子 Agent 间的间接通信

---

## 项目结构

```
penta-harness/
├── AGENTS.md                              # 入口文件（Agent 必读）
│
├── skills/                                # Skill 规则（Markdown，Agent 自觉遵守）
│   ├── liquid-cluster.md                  #   液态集群：4 阶段生命周期 + 知识注入
│   ├── wiki-knowledge.md                  #   Git Wiki：Karpathy LLM Wiki + Git 升级 + YOYO
│   ├── memory-system.md                   #   记忆系统：4 层记忆架构
│   ├── memory-inheritance.md              #   继承制记忆（memory-system 子模块）
│   ├── sub-agent-archiver.md              #   白盒归档：执行轨迹持久化
│   └── gepa.md                            #   GEPA 进化：Skill 自动优化
│
├── plugins/                               # Plugin 执行层（Python，通过钩子强制执行）
│   ├── sub-agent-archiver/                #   白盒归档执行 [priority: 100]
│   ├── liquid-cluster/                    #   集群管理执行 [priority: 50]
│   ├── wiki-manager/                      #   Wiki 管理执行 [priority: 40]
│   ├── memory-inheritance/                #   继承记忆执行 [priority: 35]
│   └── memory-system/                     #   记忆系统执行 [priority: 30]
│
└── tools/                                 # 独立 CLI 工具（框架无关）
    └── gepa/                              #   GEPA 进化引擎
```

---

## 快速开始

### 方式一：仅 Skill 规则（轻量）

将 `skills/` 目录复制到 Agent 的 Skill 目录，Agent 会自觉遵守规则：

```bash
# Hermes Agent
cp -r skills/* ~/.hermes/skills/

# Claude Code
cp -r skills/* .claude/skills/
```

### 方式二：Skill + Plugin（推荐）

两个都安装，Agent 既知道规则，又无法跳过：

```bash
# Hermes Agent
cp -r skills/* ~/.hermes/skills/
cp -r plugins/* ~/.hermes/plugins/
hermes plugins list
```

### 方式三：GEPA 进化（所有框架通用）

GEPA 是独立 CLI 工具，不依赖任何框架钩子：

```bash
# 运行一次进化分析
penta-harness gepa run

# 查看待审核建议
penta-harness gepa pending

# 应用建议
penta-harness gepa apply <id>
```

---

## 核心概念

### 子 Agent 生命周期

```
💧 临时态 (transient)     使用 < 3 次
     │
     │ 使用 ≥ 3 次
     ▼
🌱 候选态 (candidate)     开始积累知识
     │
     │ 使用 ≥ 10 次且成功率 ≥ 80%
     ▼
🌳 常驻态 (permanent)     集群固定成员，知识完整注入
     │
     │ 归档 ≥ 20 条且 GEPA 条目 ≥ 5
     ▼
🚀 进化态 (evolved)       GEPA 优化后的 Skill，可分享给其他 Agent
```

### 系统架构

```
AGENTS.md（入口）
    │
    ├── skills/（规则层）          ← Agent 自觉遵守
    │   ├── liquid-cluster        ← 集群管理
    │   ├── wiki-knowledge        ← 知识库
    │   ├── memory-system         ← 记忆系统
    │   ├── memory-inheritance    ← 继承机制
    │   ├── sub-agent-archiver    ← 归档规则
    │   └── gepa                  ← 进化规则
    │
    ├── plugins/（执行层）         ← 钩子强制执行（Hermes Agent）
    │   ├── sub-agent-archiver    [priority: 100] 最先执行
    │   ├── liquid-cluster        [priority: 50]
    │   ├── wiki-manager          [priority: 40]
    │   ├── memory-inheritance    [priority: 35]
    │   └── memory-system         [priority: 30]
    │
    └── tools/（独立工具）         ← CLI 手动触发（所有框架）
        └── gepa                  ← 进化引擎
```

### 两大独立系统

| 维度 | 记忆系统 (.memory/) | Wiki (wiki/) |
|------|---------------------|--------------|
| 本质 | 对话级经验积累 | 文档级结构化知识 |
| 内容 | Agent 的工作经验、项目记忆 | 环境信息、模式库、术语表 |
| 版本管理 | 无（或可选 Git） | Git + YOYO（推荐） |
| 关系 | 独立 | 独立 |

---

## CLI 命令

### 集群管理

```bash
hermes cluster list                    # 查看所有 Agent
hermes cluster show <agent-id>         # 查看详情
hermes cluster promote <agent-id>      # 手动升级
hermes cluster demote <agent-id>       # 手动降级
hermes cluster retire <agent-id>       # 手动淘汰
hermes cluster stats                   # 集群统计
```

### 归档管理

```bash
hermes library list                    # 查看归档记录
hermes library show <task-id>          # 查看完整轨迹
hermes library search --tool terminal  # 搜索归档
hermes library stats                   # 归档统计
```

### Wiki 知识库

```bash
hermes wiki init                       # 初始化 Wiki
hermes wiki status                     # 查看状态
hermes wiki log                        # 查看变更历史
hermes wiki show <file>                # 查看文件
hermes wiki lint                       # 健康检查
```

### 记忆系统

```bash
hermes memory init                     # 初始化记忆目录
hermes memory status                   # 查看状态
hermes memory index                    # 查看索引目录
hermes memory show project             # 查看项目记忆
hermes memory show <agent-id>          # 查看 Agent 专业记忆
```

### GEPA 进化（独立 CLI）

```bash
penta-harness gepa run                 # 运行进化分析
penta-harness gepa candidates          # 查看进化候选
penta-harness gepa pending             # 查看待审核建议
penta-harness gepa show <id>           # 查看建议详情
penta-harness gepa apply <id>          # 应用建议
penta-harness gepa reject <id>         # 拒绝建议
penta-harness gepa history             # 查看进化历史
penta-harness gepa stats               # 查看统计
```

---

## 模块说明

### liquid-cluster — 液态集群

子 Agent 不是用完即弃的工具，而是可以"转正"的集群成员。

- 4 阶段生命周期：临时 → 候选 → 常驻 → 进化
- 父 Agent 同时充当 IM 路由器 + 集群管理员
- 知识注入从 Wiki 读取，按 Agent 状态分级
- 联动 memory-system（固化时创建专业记忆）

### wiki-knowledge — Git Wiki 知识库

基于 [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 的升级方案。

- AI 自维护 Markdown 知识库
- Git 版本控制，人类随时审查、回滚
- 推荐 [YOYO](https://www.runyoyo.com/) + Git 双轨制（Agent 快照，人类 commit）

### memory-system — 四层记忆系统

| 层 | 说明 | 存储 |
|----|------|------|
| 长期记忆 | 所有 Agent 共享 | `.memory/project-memory.md` |
| 专业记忆 | 仅固化 Agent 独享 | `.memory/agents/<id>.md` |
| 执行日志 | 每个 Agent 独立 | archiver 归档数据 |
| 索引目录 | 父 Agent 自动维护 | `.memory/INDEX.md` |

### sub-agent-archiver — 白盒归档

每次子 Agent 执行的完整轨迹被持久化保存。

- 7 步归档流程：解析 → 脱敏 → 存储 → 索引 → 摘要 → GEPA 筛选
- 完整轨迹格式：thinking / tool_call / tool_result / error / correction / final_answer
- 敏感信息自动脱敏（API Key、密码、私钥）

### gepa — Skill 自动进化

独立可选模块，从归档数据中提取高价值模式，生成 Skill 优化建议。

- **框架无关**：不依赖任何框架钩子，所有框架通用
- **3 阶段流程**：原料筛选 → 模式提取 → 建议生成
- **人类审核**：建议生成到 `.gepa/pending/`，手动 apply/reject
- **统计驱动**：高效路径、避坑规则、工具组合模式

---

## 设计理念

### Skill + Plugin 双层架构

| 层 | 形式 | 作用 |
|----|------|------|
| **Skill** | Markdown 规则 | 交通法规 — Agent 自觉遵守 |
| **Plugin** | Python 代码 | 交通灯 — 钩子强制执行 |

Skill 让 Agent 知道"应该怎么做"，Plugin 确保它"无法跳过"。两者配合效果最佳。

### 记忆系统 ≠ 知识库

- **记忆系统**（.memory/）：对话级的经验积累，Agent 在工作中产生
- **Wiki**（wiki/）：文档级的结构化知识，Agent 和人类共同维护
- 两者独立但可联动

### 白盒归档 × GEPA：飞轮效应

白盒归档和 GEPA 单独看各自有价值，但联动之后产生的是**复利增长**——这就是整个系统最精妙的设计。

```
            ┌─────────────────────────────────────┐
            │           飞轮（正向循环）            │
            │                                     │
            │   归档越多 → GEPA 原料越丰富          │
            │        ↓                            │
            │   模式越清晰 → Skill 优化越精准        │
            │        ↓                            │
            │   Agent 越强 → 执行质量越高           │
            │        ↓                            │
            │   归档价值越高 → GEPA 原料更优质       │
            │        ↓                            │
            │          ↺ 循环加速                  │
            └─────────────────────────────────────┘
```

**为什么是 1+1 > 2**：

| 维度 | 只有白盒归档 | 只有 GEPA | 两者联动 |
|------|------------|----------|---------|
| 数据 | 轨迹堆积，无人分析 | 无数据可分析 | 轨迹自动成为进化原料 |
| 知识 | 静态存档，价值递减 | 无法产生建议 | 经验自动提炼为 Skill 规则 |
| Agent 能力 | 永远不变 | 永远不变 | 持续进化，越用越强 |
| 人类介入 | 需要手动翻阅归档 | — | 只需审核 GEPA 建议 |

**飞轮启动条件**：归档 ≥ 10 条同类任务后，GEPA 开始产生有价值的建议。之后每新增一条归档都在为飞轮加速。

### 液态拓扑：用规则模拟框架能力

大多数 Agent 框架的子 Agent 之间**无法直接通信**（硬编码 1 层委派，无跨 Agent 消息机制）。要实现"液态拓扑"（Agent 间自由组网），理论上需要改框架源码。

我们的解法：**不改框架，改规则。**

让父 Agent 同时充当 **IM 路由器 + 集群管理员**：

```
子 Agent A 想跟 B 协作？
  → A 把结果返回给父 Agent
  → 父 Agent 把 A 的结果注入 B 的上下文
  → B 以为这是"项目背景"，自然利用
```

子 Agent 完全不知道其他 Agent 的存在，但从效果上看，它们实现了间接协作。**用一层 Skill 规则，模拟了需要改框架才能实现的能力。**

### 独立系统通过引用联动

记忆系统、Wiki、集群管理——每个系统都是**独立可安装**的。但安装多个后，它们通过**引用关系**自动互相增强：

```
liquid-cluster  ──引用──→  archiver（归档数据）
              ──引用──→  wiki-knowledge（知识注入）
              ──联动──→  memory-system（固化时创建专业记忆）

memory-system  ──包含──→  memory-inheritance（继承子模块）
             ──关联──→  wiki-knowledge（独立但可互相引用）

gepa           ──输入──→  archiver（归档数据）
             ──输出──→  skills/*.md（优化后的 Skill）
```

**设计哲学**：每个模块都是独立的产品，合在一起是更大的产品。用户可以只用其中一个，也可以全部安装——安装越多，联动效应越强。

### GEPA 人类审核机制

GEPA 不直接修改任何文件。所有修改建议都经过人类审核：

```
GEPA 分析 → .gepa/pending/ → 人类审核 → apply/reject
```

Agent 可以自动**建议**，但人类拥有最终**决定权**。

---

## 灵感来源

- [Harness Engineering](https://github.com/nousresearch/hermes-agent) — "Agent = Model + Harness" 范式
- [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — AI 自维护知识库的基础方案
- [YOYO](https://www.runyoyo.com/) — AI 时代的影子版本控制

---

## 许可证

MIT
