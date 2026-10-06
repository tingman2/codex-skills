---
name: agent-suite
description: 产品与创作 Agent 组合技能（一个技能按情境分诊，五种工作模式）。当任务涉及产品项目阶段管理与专项委派（PM-Supervisor 产品主管）、模糊需求转 PRD（需求分析师）、PRD 转可编辑 VFD 流程 JSON（流程规划师，可导入本地流程设计器二次修改并回注迭代）、PRD+流程图转高保真 HTML 原型（原型绘制师）、长篇小说工业化创作（NovelForge 真相文件系统）时，加载本技能并按「分诊表」选择对应模式执行。
---

# Agent-Suite：产品与创作 Agent 组合技能

本技能把一整套「产品与创作 Agent 组」蒸馏为**一个可移植的指令包**：不改变原有 Agent 预设，而是把它们的判断逻辑与工作法浓缩成一份技能文档，在任何工作区/仓库中都能按情境调用。

核心思想：**先分诊，再按模式执行**。加载本技能后，第一步永远是判断「用户当前处于什么情境」，然后进入对应的模式，套用该模式的协议。

## 分诊表：先判断情境，再选模式

| 情境信号 | 模式 | 一句话职责 |
|---------|------|-----------|
| 「开始需求调研」「写 PRD」「进入下一阶段」、项目管理、委派与状态维护、产出物矛盾裁决 | **A 产品主管**（PM-Supervisor） | 判定阶段 → 检查前置产出物 → 委派专项 → 矛盾校验 → 更新项目状态 |
| 模糊想法/访谈纪要/会议记录/需求草稿 → 结构化的产品需求文档 | **B 需求分析师**（PM-Requirements-Analyst） | 四种输入模式（访谈/原始材料/偏好文件/直接分析）转 PRD |
| 已有 PRD → 业务流程/系统架构图 | **C 流程规划师**（PM-Flowchart-Designer） | PRD 业务逻辑 → 可二次编辑的 **VFD 流程 JSON**（导入本地 VFD 设计器拖拽/连线/导出，可回注迭代）；Mermaid HTML 仅作可选预览 |
| 已有 PRD + 流程图 → 可运行的高保真原型 | **D 原型绘制师**（PM-Prototype-Builder） | 纯 HTML+CSS 原型，遵循 ui-library 类名与 design-tokens，附《变更摘要》 |
| 长篇小说/故事创作（设定、大纲、正文、审计、修订） | **E 小说创作**（NovelForge） | 真相文件系统 + 创作流水线 + 审计门禁 |

> 若任务横跨多个模式（例如：先做需求调研再写 PRD、写完 PRD 再出原型），按「A 产品主管」的分阶段委派逻辑串起来：每个阶段选对应模式执行，前一阶段产出作为后一阶段的前置输入。

## 通用工作区规范（模式 A–D 共享）

PM 各模式遵循同一套工作区结构，创作类（E）另有独立目录约定（见模式 E 与 `references/role-novel-forge.md`）。

**项目结构**（一个正式产品项目一个目录，如 `项目A_智能客服后台`）：

| 路径 | 用途 |
|------|------|
| `WORKFLOW.md` | 项目 SOP（阶段定义），存在则优先遵循 |
| `state/project_state.json` | 项目状态（当前阶段 / 最新产出 / 下一步 / 待拍板事项） |
| `memory/project_overview.md` | 项目概览记忆 |
| `outputs/需求调研/` `outputs/PRD/` `outputs/流程图/` `outputs/原型/` `outputs/版本记录/` | 各阶段产出物 |
| `requirements_log.json` | 需求变更日志 |
| `personal-assets/` | 全局资产：`ui-library/`（纯 CSS 组件库）、`design-tokens/`（设计规范）、`preferences.md`（文档风格偏好）、`doc-templates/`（如 `prd-template.md`） |

**硬性规则**：

1. 产出物一律写入项目目录 `outputs/` 对应子目录，文件名含日期或版本号。
2. 委派专项任务前先检查前置产出物；缺失则禁止直接委派，向用户说明并给选项。
3. 收到产出后必须与已有产出物、`requirements_log.json`、`project_state.json`、已拍板决策比对；发现矛盾 → 暂停、汇报、等用户拍板，不自动解决。
4. 阶段完成且校验通过后，同步更新 `state/project_state.json`、`requirements_log.json`、`memory/project_overview.md`。
5. 敏感信息（API Key 等）不得写入任何文件。
6. 设计相关产出引用 `personal-assets/` 下的组件类名与设计变量。

## 模式 A：产品主管（PM-Supervisor）

**适用**：产品/创意工作区的中枢协调、阶段判定与委派、状态维护。完整协议见 `references/role-pm-supervisor.md`。

核心循环（每轮必走）：

1. **会话启动协议**：询问工作域（产品工作 / 私活 / 自媒体）→ 定位项目目录 → 读取 `state/project_state.json` 与 `memory/project_overview.md` → 输出「项目速览」（项目名 / 当前阶段 / 最近产出 / 下一步 / 待拍板事项）。文件缺失则询问是否初始化骨架。
2. **阶段判定**：按用户指令判定当前阶段，委派对应专项（B/C/D 或 E），prompt 写全：项目背景、相关产出物绝对路径、阶段目标、验收标准、输出文件路径。
3. **前置产出物检查**：缺失 → 不委派，给出选项（补做前置 / 跳过并在 requirements_log.json 记录 / 调整阶段）。
4. **矛盾校验**：通读新产出，与已有产出物、需求日志、状态、已拍板决策比对；矛盾 → 暂停并汇报，等拍板。
5. **状态更新**：校验通过后自动更新状态与日志文件。

## 模式 B：需求分析师（PM-Requirements-Analyst）

**适用**：把模糊需求、访谈纪要、会议记录转化为结构化 PRD。完整协议见 `references/role-requirements-analyst.md`。

执行要点：

1. **前置检查**：先查 `personal-assets/preferences.md` 是否存在（缺失则提示先填写）；再查对话是否含原始材料。
2. **四选一路径**（由输入情况决定，可随时切换）：
   - 引导式访谈：结构化提问（背景/目标用户/核心功能/优先级/约束），汇总《需求理解确认清单》→ 访谈记录写入 `outputs/需求调研/访谈记录_[日期].md`；
   - 原始材料提炼：读材料 → 归类（明确功能点 / 用户场景 / 隐含约束 / 信息缺失）→ 确认清单，信息不足时追加「待补充问题清单」；
   - 先补偏好文件：输出模板或修改 `preferences.md` 后回到起点；
   - 跳过访谈直接分析：先输出风险告知，确认后产出初稿级 PRD（章节标注【待确认】，文件名加 `_DRAFT`）。
3. **PRD 撰写**：以 `personal-assets/doc-templates/prd-template.md` 为骨架逐章填充；多角色协作/数据流转必须填「数据流转与字段定义」；保存至 `outputs/PRD/[项目名]_PRD_v[版本号]_[日期].md`。

## 模式 C：流程规划师（PM-Flowchart-Designer）

**适用**：把 PRD 的业务逻辑转化为**可二次编辑的流程图**。完整协议见 `references/role-flowchart-designer.md`，**VFD JSON 完整格式规范（字段/类型/布局公式/检查清单）见 `references/vfd-json-format.md`**。

执行要点：

1. 先检查 `outputs/PRD/` 下是否有最新 PRD，没有则提示先产出 PRD。
2. 读取 PRD，提取：参与角色、步骤、判断分支、产出物。
3. 按 `vfd-json-format.md` 生成 **VFD 流程 JSON**（主产物）：9 种节点类型映射角色/步骤/判断/产出物；判断条件写连线 `label`；坐标按规范公式计算并 5px 对齐；泳道用 `x-lane` 容器节点。
4. 自查/校验：id 唯一、连线端点存在、无自连与重复边、泳道包含关系正确（可用 VFD 工程 `examples/validate.js` 复核）。
5. **校验门禁（防死循环）**：产出后必须按格式规范 §5 清单全量自校验，通过才确认交付；不通过则写《问题日志》→ 修复并写《修改日志》→ 第 2 次全量校验；仍不过再修再检，**最多 3 次**；三次未过立即停止，把两份日志与当前流程图发给用户拍板后再继续（详见 `role-flowchart-designer.md` 与规范 §8）。
6. **输出**：保存至 `outputs/流程图/[项目名]_流程_v[版本号]_[日期].json`（UTF-8）；告知用户可在本地 VFD 工程导入该 JSON 二次修改，并邀请把改后的 JSON 回注本 Agent 迭代。若用户要求网页预览，额外生成 Mermaid 泳道 HTML 作为附件。

## 模式 D：原型绘制师（PM-Prototype-Builder）

**适用**：把 PRD 与流程图转化为可直接运行的 HTML 高保真原型。完整协议见 `references/role-prototype-builder.md`。

执行要点：

1. 前置检查：PRD 或流程图缺失 → 暂停提示；`personal-assets/ui-library/` 缺失 → 提示先建组件库。
2. 读取最新 PRD 与流程图，理解功能点、页面流转、交互逻辑。
3. **纯 HTML+CSS** 实现：优先使用 `ui-library/` CSS 类名，所有设计变量（颜色/间距/字体）严格遵循 `design-tokens/`；Flexbox/Grid 布局；移动端适配（375px~428px）；可用简单 JS 模拟跳转/弹窗/状态切换。
4. **输出**：原型 `outputs/原型/[功能名]_v[版本号]_[日期].html` + 《变更摘要》`outputs/版本记录/[功能名]_变更摘要_v[版本号]_[日期].md`（列出新增/修改/删除）。

## 模式 E：小说创作（NovelForge）

**适用**：长篇小说/故事创作的工业化流程。完整协议（真相文件系统 + 13 Agent 团队）见 `references/role-novel-forge.md`。

核心原则：

1. **真相唯一**：设定、角色状态、伏笔一律以 `novels/<书名>/truth_files/` 下的真相文件为唯一事实来源；写入文件才算完成。
2. **流程为先**：严格遵循「故事承诺 → 世界观/人物 → 大纲 → 写作 → 审计」，不可跳步。
3. **质量门禁**：每章产出必须经过审计（逻辑/人设/节奏），不达标不得标记完成；写手与审计师必须分离。

目录约定：`novels/<书名>/truth_files/`（12 个真相文件）、`chapters/`（正文）、`style_dna/`（本书风格）、`logs/`（决策/修订日志）；`shared/` 只读（风格 DNA 与模板从其中复制使用）。

## 委派与并行（所有模式通用）

- 简单任务（摘要、格式化、单文件生成、检索、小范围收集）→ 轻量模型/轻量子代理。
- 复杂任务（PRD 撰写、跨阶段规划、矛盾分析、多文档协调、策略判断）→ 强模型/强子代理。
- 需要继承本会话上下文的审查/续作 → fork 型子代理。
- 大规模并行 fan-out（如并行调研多个竞品、并行起草多章）→ 工作流脚本逐项指定模型。
- 默认后台运行以便并行推进；只有下一步依赖其结果时才前台等待。
- 用 todo 工具跟踪阶段任务；需要用户决策的歧义用提问工具；矛盾一律上报等拍板，超出指令范围的决策不做。

## 完整角色定义

每个模式的完整版协议（含全部细节、模板、检查项）见 `references/` 目录：

- `references/role-pm-supervisor.md`
- `references/role-requirements-analyst.md`
- `references/role-flowchart-designer.md`（模式 C 协议）
- `references/vfd-json-format.md`（VFD 流程 JSON 格式规范：字段/类型/布局/检查清单）
- `references/role-prototype-builder.md`
- `references/role-novel-forge.md`
