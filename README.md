# Research Learning Loop

面向 AI、3D/4D Vision 与 World Models 初学者的研究学习 Skill。

它把新领域入门、论文阅读、前置知识补全、官方代码追踪、论文—代码映射、项目复现、实验验证和主动回忆连接成一个可恢复的学习闭环。

当前版本：`v0.4.0`

## 它解决什么问题

面对论文和大型代码仓库时，初学者常常会遇到这些问题：

- 不知道进入新领域需要先建立什么知识地图；
- 论文涉及大量前置知识和引用，不知道先读哪里；
- 仓库文件很多，不知道真实入口、配置覆盖和执行路径；
- 代码能够运行，却不知道是否真的复现了论文主张；
- 完成一次阅读或运行后，没有形成可迁移的理论和代码能力。

Research Learning Loop 以学习者成长为目标，不默认替用户生成整份实现，也不把“跑通”当作“复现成功”。

## 核心流程

```text
S0 目标、协作方式与来源锁定
↓
S1 最小领域地图与锚点材料
↓
S2 论文第一遍固定阅读
↓
S3 阻塞性前置知识桥
↓
S4 机制重建与主张审计
↓
S5 真实执行路径与实现映射
↓
S6 复现契约与实验设计
↓
S7 执行、验证与失败诊断
↓
S8 主动回忆、能力更新与下一步
```

这不是强制流水线。Skill 会根据目标从合适阶段开始，只补齐真正阻塞的前置环节。

## 三遍论文阅读

1. **建图**：按固定顺序建立论文全局地图。
2. **重建**：定向深读核心机制、公式和主张—证据关系。
3. **核验**：在代码追踪或复现时，核对论文、官方实现和实验行为。

只有第一遍是完整的顺序阅读；后两遍都是问题驱动的定点深读。仅学习论文时通常读两遍，进行论文—代码映射或复现时通常读三遍。

## 六种使用方式

- `enter-field`：进入一个陌生研究领域。
- `learn-paper`：理解一篇论文。
- `trace-code`：追踪一个仓库的真实执行路径。
- `paper-code-map`：建立论文机制和代码实现的映射。
- `reproduce`：分级复现并验证论文主张。
- `consolidate`：通过 teach-back、自测和下一步设计巩固能力。

## 示例提示词

```text
使用 $research-learning-loop 带我进入 4D Gaussian Splatting，先建立最小领域地图，不运行代码。
```

```text
使用 $research-learning-loop 按固定第一遍顺序带我阅读这篇论文；遇到阻塞概念时建立知识桥。
```

```text
使用 $research-learning-loop 从 README 命令开始，追踪 Eq. 7 的 loss 到真实反向传播路径，并标注 tensor shape 和生效配置。
```

```text
使用 $research-learning-loop 在两小时和 24GB 显存限制内，先复现官方 demo，再验证一个最小机制主张。
```

## 安装

将仓库克隆到支持 `SKILL.md` 的 Agent Skills 目录。例如在 Codex 中：

```bash
git clone https://github.com/ZhengyangZhang1107/research-learning-loop.git ~/.codex/skills/research-learning-loop
```

也可以将本仓库作为项目级 Skill 使用。入口文件是 [`SKILL.md`](SKILL.md)。

## 仓库结构

```text
research-learning-loop/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── field-and-paper.md
    ├── code-and-mapping.md
    ├── reproduction-and-validation.md
    ├── schemas.md
    ├── domain-checks.md
    └── design-provenance.md
```

`SKILL.md` 只保存路由、共享状态机和关键不变量；详细方法按当前任务从 `references/` 中渐进加载。

## 设计原则

- 学习优先：保留用户亲自解释、预测、实现或诊断的环节。
- 证据优先：区分作者主张、论文证据、实现证据、实验观察和推断。
- 单一事实来源：主张、实现、复现目标和单次运行分别只维护一次。
- 最小可信实验：先验证最小纵向闭环，再增加规模和成本。
- 可恢复：通过稳定 ID 和派生交接视图继续上一次学习，而不是重新开始。

开源设计来源及借鉴边界见 [`references/design-provenance.md`](references/design-provenance.md)。

## License

MIT
