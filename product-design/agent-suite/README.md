# Agent-Suite（agent-suite）

产品与创作 Agent 组合技能：**一个技能，按情境分诊，五种工作模式**。

本文件夹是把整套「产品与创作 Agent 组」蒸馏成的可移植指令包，可整目录上传到你的仓库，
也可直接装回 DSH 作为技能使用。**它不改变、不依赖原有的 Agent 预设**——预设仍在你
本机 `~/.dsh/.agent-presets/` 下原样运行，本技能是额外的一份可复用资产。

## 目录结构

```
agent-suite/
├── SKILL.md                    # 主技能文件（分诊路由 + 通用规范 + 五模式速览）
├── README.md                   # 本说明
└── references/
    ├── role-pm-supervisor.md           # 模式 A：产品主管（完整协议）
    ├── role-requirements-analyst.md    # 模式 B：需求分析师（完整协议）
    ├── role-flowchart-designer.md      # 模式 C：流程规划师（完整协议）
    ├── vfd-json-format.md              # 模式 C 配套：VFD 流程 JSON 格式规范
    ├── role-prototype-builder.md       # 模式 D：原型绘制师（完整协议）
    └── role-novel-forge.md             # 模式 E：小说创作（完整协议）
```

## 五种模式（分诊表）

| 情境信号 | 模式 | 职责 |
|---------|------|------|
| 项目管理、阶段委派、矛盾裁决、状态维护 | A 产品主管 | 判定阶段 → 前置检查 → 委派 → 矛盾校验 → 更新状态 |
| 模糊需求/访谈纪要/会议记录 → PRD | B 需求分析师 | 四种输入路径转结构化 PRD |
| PRD → 业务流程/架构图 | C 流程规划师 | **VFD 流程图 JSON**（可导入本地设计器二次编辑并回注迭代）；Mermaid HTML 作可选预览 |
| PRD+流程图 → 可运行原型 | D 原型绘制师 | 纯 HTML+CSS 高保真原型 + 变更摘要 |
| 长篇小说/故事创作 | E 小说创作 | 真相文件系统 + 创作流水线 + 审计门禁 |

详细规则以 `SKILL.md` 的分诊表与 `references/` 下各角色文件为准。

## 使用方式

### 在 DSH 中使用（推荐）

把本文件夹放到 DSH 的技能发现目录之一，重启/刷新后技能目录中会出现 `agent-suite`：

- **用户级**（所有会话可用）：`~/.dsh/skills/agent-suite/`
- **项目级**（仅该项目会话可用）：`<你的仓库>/.dsh/skills/agent-suite/`

即复制本文件夹为 `<目标目录>/agent-suite/`（含 `SKILL.md` 与 `references/`），
DSH 会自动扫描并加载。

### 作为普通指令文档使用

任何支持「技能/指令包」的 Agent 环境，直接把 `SKILL.md` 作为技能指令加载，
`references/` 作为其引用附件即可；也可手动把 `SKILL.md` 内容粘贴进会话。

## 与原有 Agent 预设的关系

| | DSH Agent 预设（`~/.dsh/.agent-presets/`） | 本技能 |
|---|---|---|
| 形态 | Cordis 组合（persona + 工具行 + 模型路由），创建会话时选择 | 纯指令文档（Markdown） |
| 运行 | 独立会话，自带工具集与结构化模型路由 | 加载到任意会话，行为由指令驱动 |
| 改动 | 本技能**不修改**任何预设文件 | 独立文件夹，可随时删除 |

两者职责互补：预设提供「可运行的 Agent 会话」，技能提供「可移植的方法论」。
本技能的行为描述源自以下 5 个预设：`pm-supervisor`、`pm-requirements-analyst`、
`pm-flowchart-designer`、`pm-prototype-builder`、`novel-forge`。

## 自定义

- 改分诊逻辑或模式速览：编辑 `SKILL.md`。
- 改某个角色的完整协议：编辑 `references/` 对应文件。
- 新增模式：在 `references/` 加角色文件，并在 `SKILL.md` 分诊表与速览中登记。
