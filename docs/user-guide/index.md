# 用户文档

这一部分只面向“要把系统用起来的人”。

这里不优先解释底层架构、状态合同或模块设计，而是优先回答：

- 第一次怎么安装和启用。
- 该用 `/auto-research` 还是 `/auto-review`。
- 项目卡住时先看哪里。
- 会话断了以后怎么恢复。

## 推荐阅读顺序

1. [10 分钟快速上手教程](./quickstart-tutorial.md)
2. [安装与启用](../get-started/installation.md)
3. [项目生命周期](../get-started/project-lifecycle.md)

## 什么时候看这一部分

- 你是第一次接触 `ClawAutoResearch`
- 你想先把一个实验项目或综述项目跑起来
- 你不想先读控制平面和运行时细节

## 什么时候跳去技术文档

如果你要做下面这些事，就转到 [技术文档](../technical/index.md)：

- 排查 workflow runtime 为什么没继续推进
- 修改 stage gate、handoff、mailbox、PaperNexus 路由
- 理解 `research_workflow`、状态合同或模块边界
