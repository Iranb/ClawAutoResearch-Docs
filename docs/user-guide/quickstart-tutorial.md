# 10 分钟快速上手教程

这篇文档只回答一件事：

“我第一次用 `ClawAutoResearch`，要怎么尽快把一个项目跑起来？”

不讲架构细节，不展开状态机设计，只给你一条最短可操作路径。

## 你会得到什么

做完这篇教程，你应该能完成这 4 件事：

1. 确认插件已经正确安装。
2. 用一个主题自动创建项目。
3. 知道实验项目和综述项目该用哪个命令。
4. 在会话中断后用正确方式恢复，而不是继续翻聊天记录。

## 第 0 步：先确认环境可用

在仓库根目录执行：

```bash
npm install
bash install.sh
```

如果你是在 OpenClaw / Discord / workflow-enabled channel 里使用，还需要确认：

- 插件已经被加载。
- 当前会话有工作流工具权限。
- 你不是在一个“只会发普通聊天消息、不会触发 workflow runtime”的假入口里测试。

如果你只是想先看本地文档站：

```bash
npm run docs:dev
```

## 第 1 步：先选项目类型

你只需要先分清两条主线：

### A. 实验论文主线

适合：

- 你要提出新方法
- 你要写代码、跑实验、分析结果
- 最后要形成方法论文

入口命令：

```text
/auto-research "你的主题"
```

例子：

```text
/auto-research "confirmation bias mitigation for generalized category discovery"
```

### B. 科研综述主线

适合：

- 你要做 survey / review
- 你要先收集文献、做 screening、coverage、gap synthesis
- 最后写的是综述论文，不是实验方法稿

入口命令：

```text
/auto-review "你的主题"
```

例子：

```text
/auto-review "generalized category discovery survey"
```

> [!TIP]
> 如果你的目标是综述，不要先走 `idea -> plan -> code -> experiment` 那条默认实验路径。直接从 `/auto-review` 或 `/survey-pipeline` 开始。

## 第 2 步：让系统自动建项目

无论你走哪条主线，第一次都不需要手工搭骨架。

系统会自动创建最小项目结构，常见包括：

- `PROJECT_MANIFEST.json`
- `TRACK_REGISTRY.json`
- `CLAIM_POLICY.md`
- `researcher/EXPERIMENT_LEDGER.json`
- `.openclaw-research/` 运行时状态目录

此时你不用先看所有文件。只要确认两件事：

1. 项目目录已经创建出来。
2. `PROJECT_MANIFEST.json.current_stage` 不再是空的。

## 第 3 步：先看状态，不要猜状态

项目启动后，第一反应不是继续口头问“下一步做什么”，而是看 durable state：

```text
/workflow-status
```

如果你在工具侧，优先看：

- `PROJECT_MANIFEST.json`
- `.openclaw-research/workflow-runtime-queue.json`
- `.openclaw-research/workflow-events.jsonl`

你重点关注这几个字段：

- `current_stage`
- `current_micro_stage`
- `owner_agent`
- `next_action`
- `blocking_reason`

## 第 4 步：理解“卡住”时最常见的 3 种情况

### 情况 1：实验项目卡在 `setup`

这通常不是 bug，而是 onboarding 还没补齐。

优先看：

- `research_program.goal`
- `baseline_reference`
- `primary_metric`
- `datasets`
- `success_criteria`
- `zotero_project_path`

### 情况 2：一直回到 `graph_build`

这通常说明 shared graph 还没 ready，不是系统保守过度。

优先看：

- `paper_ingestion.graph_presence_status`
- `graph/GRAPH_PRESENCE_CHECK.json`
- `graph/GRAPH_BUILD_REPORT.md`

### 情况 3：综述项目停在 `survey_review`

先不要怀疑写作链路，先看 survey packet 是否真的齐了。

优先看：

- `researcher/SURVEY_QUERY_REGISTRY.json`
- `researcher/INCLUDED_PAPERS.json`
- `researcher/EXCLUDED_PAPERS.json`
- `researcher/LITERATURE_REVIEW.md`
- `researcher/GAP_SYNTHESIS.md`
- `researcher/SURVEY_BRIEF.md`

## 第 5 步：会话断了以后怎么恢复

正确恢复方式是：

```text
/resume-pipeline
```

而不是：

- 继续沿着旧聊天历史往下说
- 凭记忆喊下一个 agent 干活
- 手动猜当前 stage

恢复时，系统应该重新从 durable state 推断现场，而不是依赖聊天上下文。

## 第 6 步：一条真正够用的最短路线

### 实验项目

```text
安装插件
  -> /auto-research "topic"
  -> /workflow-status
  -> 看 blocking_reason / next_action
  -> /resume-pipeline
```

### 综述项目

```text
安装插件
  -> /auto-review "topic"
  -> /workflow-status
  -> 看 survey_review packet 是否开始 materialize
  -> /resume-pipeline
```

## 第 7 步：什么时候再去读更细的文档

等你完成上面流程以后，再按下面顺序深入：

1. [安装与启用](../get-started/installation.md)
2. [项目生命周期](../get-started/project-lifecycle.md)
3. [Workflow 控制平面](../architecture/workflow-control-plane.md)

如果你是维护者，再继续看：

1. [技术文档入口](../technical/index.md)
2. [State Contracts](../reference/state-contracts.md)
3. [Module Map](../reference/module-map.md)

## 最后给第一次使用者的建议

- 先跑起来，再理解全貌。
- 先看 durable state，再问“为什么卡住”。
- 先分清实验主线和综述主线，不要混用入口。
- 会话断了就 `resume`，不要靠聊天历史续命。
