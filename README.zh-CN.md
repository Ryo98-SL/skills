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

## 仓库结构

```text
.
├── README.md
├── README.zh-CN.md
├── code-style-guardrails/
│   ├── SKILL.md
│   └── references/
│       └── index-md-template.md
└── package-guardrails/
    ├── SKILL.md
    └── references/
        ├── issue-workflow.md
        ├── path-conventions.md
        └── role-rules.md
```

## 安装方式

本仓库遵循 Vercel Labs `skills` CLI 所支持的 open agent skills ecosystem。

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/package-guardrails -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/code-style-guardrails -a codex
```

安装后，当任务涉及 package-based repository 内的实现、评审、修 bug、加功能或跨 package issue 交接时，Codex 就可以使用 `package-guardrails`。当任务涉及 TypeScript、TSX、React、模块结构、样式一致性或文档同步时，Codex 就可以使用 `code-style-guardrails`。
