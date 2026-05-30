# Ryo98 的 Skills

这是一个个人 Codex skills 仓库，用来约束 AI 编码 agent 的工作边界，让它们在大型仓库里更专注、更可控，也更容易并行协作。

[English](README.md)

## 当前可用的 Skill

### package-guardrails

`package-guardrails` 适用于按 package、workspace 或模块划分边界的仓库，核心目标是让 agent 始终围绕一个明确的 package 工作。

它主要解决这些问题：

- 在开始工作前要求明确 `owner_package`，减少无关上下文输入；
- 将每个 agent 的可写范围限制在单个 package 内；
- 编码前要求读取正确的 package 文档；
- 避免 agent 误改不属于自己的 package；
- 当一个 package 依赖另一个 package 的能力或修复时，通过 issue handoff 交接，而不是跨边界直接修改；
- 通过 `README.md` 和 `README.deep.md` 保留 package 级别的现状说明，方便新对话里的 agent 快速接续工作。

这个 skill 特别适合多 agent 并行开发：每个 agent 只拥有一个 package，把其他 package 当作只读依赖；如果依赖方缺少能力或存在 bug，就创建结构化 issue 交给对应 package 的 owner agent 处理。

完整规则请查看 [`package-guardrails/SKILL.md`](package-guardrails/SKILL.md)。

### code-style-guardrails

`code-style-guardrails` 用来为实现和重构工作约束仓库本地的代码结构、前端样式约定和文档同步规则。

它主要解决这些问题：

- 在编辑前要求 agent 先识别目标 package、app、module、feature folder 或 component folder；
- 编码前要求读取附近的仓库文档和既有约定；
- 让 TypeScript 和 TSX 改动按职责拆分，避免单文件持续膨胀成混杂多种关注点的大文件；
- 让前端样式跟随目标项目已有体系，无论项目使用 Tailwind、CSS modules、CSS-in-JS、design-system props 还是普通 CSS；
- 当行为、安装方式、命令或结构变化时，同步更新面向用户和面向实现的文档；
- 鼓励使用仓库自身的 lint、typecheck、test 或 style guard 命令做聚焦验证。

这个 skill 适用于通用 TypeScript 和 React 项目，包括 monorepo、app 目录、package 目录以及按 feature 组织的代码库。它不绑定具体产品、框架或样式栈；本地约定优先。

完整规则请查看 [`code-style-guardrails/SKILL.md`](code-style-guardrails/SKILL.md)。

### task-chain-planner

`task-chain-planner` 用来把 feature design、重构、研究任务或项目拆成有明确依赖顺序、可以独立执行和验收的任务链。

它主要解决这些问题：

- 按依赖边界拆分高层工作，而不是按文件列表机械拆分；
- 让另一个 engineer 或 agent 不依赖聊天历史也能接续执行；
- 要求每个任务都有清晰的 brief、handoff document 和 acceptance document；
- 让下游任务依赖持久化 handoff 文档，而不是隐含上下文；
- 通过验证命令和人工检查点明确每个任务的完成门槛。

这个 skill 适合处理无法安全地一次性实现的大型功能、重构或项目。它负责生成持久化规划文档，并在用户没有明确要求继续实现时停在规划阶段。

完整规则请查看 [`task-chain-planner/SKILL.md`](task-chain-planner/SKILL.md)。

### mainline-grill-me

`mainline-grill-me` 用来围绕一个计划或设计进行主线式追问：先解决主要设计分支，对次要实现细节给出最佳实践默认值。

它主要解决这些问题：

- 在开始实现或细化规划前，让用户和 agent 先达成共同理解；
- 每次只追问一个主要设计分支；
- 对每个主要问题给出推荐答案，方便用户直接接受、修正或反驳；
- 如果问题能通过阅读代码库回答，就让 agent 先探索代码库；
- 对琐碎实现细节不逐项追问，而是列出默认做法和简短理由；
- 持续记录已接受的决策，并用这些决策约束后续问题。

这个 skill 适合在计划还需要被压实、但又不想陷入所有小选项时使用。它会把讨论保持在设计主线上，同时留下足够明确的决策，方便 engineer 或 agent 后续执行。

完整规则请查看 [`mainline-grill-me/SKILL.md`](mainline-grill-me/SKILL.md)。

## 仓库结构

```text
.
├── README.md
├── README.zh-CN.md
├── code-style-guardrails/
│   ├── SKILL.md
│   └── references/
│       └── index-md-template.md
├── mainline-grill-me/
│   └── SKILL.md
├── package-guardrails/
│   ├── SKILL.md
│   └── references/
│       ├── issue-workflow.md
│       ├── path-conventions.md
│       └── role-rules.md
└── task-chain-planner/
    ├── SKILL.md
    └── references/
        └── templates.md
```

## 安装方式

本仓库遵循 Vercel Labs `skills` CLI 所支持的 open agent skills ecosystem。

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/package-guardrails -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/code-style-guardrails -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/task-chain-planner -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/mainline-grill-me -a codex
```

安装后，当任务涉及 package-based repository 内的实现、评审、修 bug、加功能或跨 package issue 交接时，Codex 就可以使用 `package-guardrails`。当任务涉及 TypeScript、TSX、React、模块结构、样式一致性或文档同步时，Codex 就可以使用 `code-style-guardrails`。当一个高层设计或项目需要拆成可恢复、可交接、可验收的任务链时，Codex 就可以使用 `task-chain-planner`。当一个计划或设计需要围绕关键决策做主线式追问时，Codex 就可以使用 `mainline-grill-me`。
