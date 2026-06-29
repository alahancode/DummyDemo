# OSINT Agent Console Demo Implementation Task Plan

> For AI coding agent: do not start by inventing requirements. First read `docs/demo_brief.md` and `docs/frontend_spec.md`, then implement the single-file HTML demo according to this task plan.

## 1. Task Scale

**Scale: small**

Reason:

- The deliverable is one static HTML file.
- CSS and JavaScript are inline.
- No backend, database, build tool, package install, external API, or real LLM integration is required.
- The main complexity is interaction sequencing, clear mock boundaries, and professional security-console visual polish.

## 2. Clarifying Questions

No clarification is required before execution.

The project already defines the product context and frontend constraints in:

- `docs/demo_brief.md`
- `docs/frontend_spec.md`

## 3. Assumptions

- Output file name: `osint_agent_console_demo.html`.
- All OSINT source results, execution logs, report content, and chat replies are local mock data.
- The page must clearly state that no external OSINT API is called.
- Chat is simulated with predefined responses, not a real LLM.
- The demo is optimized for desktop/laptop presentation.
- Mobile only needs to remain readable and non-broken.
- Do not introduce React, Vite, Tailwind, backend services, npm packages, or build tooling.

## 4. Atomic Tasks

| task_id | 目标 | 输入 | 输出 | 涉及文件或模块 | 前置依赖 | 完成标准 | 测试方法 | 风险点 | 是否可以并行 |
|---|---|---|---|---|---|---|---|---|---|
| T1 | 读取并锁定需求边界 | `docs/demo_brief.md`, `docs/frontend_spec.md` | 一份实现前上下文摘要，明确目标、边界、页面结构、交互、验收标准 | 只读：`docs/demo_brief.md`, `docs/frontend_spec.md` | 无 | 摘要明确包含：single HTML、inline CSS/JS、mock-only、no external API、simulated chat、security console style | 人工检查摘要是否覆盖 Brief 和 SPEC 的关键限制 | 没读完整文档，导致后续实现偏成 landing page 或真实后端假象 | 否 |
| T2 | 创建单文件 HTML 基础骨架 | T1 摘要 | `osint_agent_console_demo.html` 初始文件，包含 HTML/head/body/style/script 区域 | 创建：`osint_agent_console_demo.html` | T1 | 文件可直接用浏览器打开；页面标题正确；无外部构建依赖；控制台无报错 | 双击打开 HTML；浏览器 DevTools 检查 console | 过早引入外部依赖或构建工具 | 否 |
| T3 | 搭建专业安全工作台布局 | Frontend SPEC 页面结构与视觉要求 | 顶部 command bar、左侧 execution log、中间 source/report、右侧 Agent Lab/chat 的三栏布局 | 修改：`osint_agent_console_demo.html` 的 HTML/CSS | T2 | 第一眼像安全分析工具；不是 SaaS 官网；无大 hero；文本不重叠；卡片半径不超过 8px | 浏览器打开检查 1440px 和 1280px 宽度；确认布局稳定 | 视觉做成营销页、模板站或过度装饰 | 否 |
| T4 | 定义集中 mock 数据结构 | Demo Brief 核心场景、Frontend SPEC 数据策略 | `demoInvestigation` mock fixture，包含 IOC、sources、executionSteps、report、chatResponses、limitations | 修改：`osint_agent_console_demo.html` 的 inline JS | T2 | 所有演示数据集中维护；字段覆盖 source raw result、normalized signals、reasoning notes、suggested action、report、chat replies | 搜索文件，确认主要 mock 文案来自集中数据对象 | mock 字段被误当成真实后端 contract；数据散落在 DOM 操作里 | 可与 T3 并行 |
| T5 | 渲染初始空状态 | T3 布局、T4 mock 数据 | 初始页面：IOC 输入可用，source cards idle，log ready/empty，report placeholder，Agent Lab locked，chat disabled | 修改：`osint_agent_console_demo.html` 的 HTML/JS/CSS | T3, T4 | 页面初始状态符合 SPEC；默认 IOC 可为 `185.220.101.47`；边界 badge 可见 | 打开页面不点击 Run，逐项检查初始状态 | 初始页面信息太空，观众不知道这是调查工作台 | 否 |
| T6 | 实现 Run Investigation 状态流程 | executionSteps、source 状态设计 | 点击 Run 后输入锁定、按钮禁用、execution log 逐步追加、运行状态可见 | 修改：`osint_agent_console_demo.html` 的 inline JS | T5 | Run 后有明显过程感；不会重复启动多个调查；log 至少 6 条逐步出现 | 快速多次点击 Run；观察是否只有一个流程运行 | timeout 状态混乱；重复点击导致日志/状态叠加 | 否 |
| T7 | 实现 source cards 状态变化 | sources mock fixture、T6 流程 | source cards 从 idle/querying/done/flagged/error 变化，并展示状态 badge 与风险色 | 修改：`osint_agent_console_demo.html` 的 HTML/JS/CSS | T6 | 至少 4 个 source card；状态随调查推进变化；flagged source 有明显但克制的视觉提示 | 点击 Run，观察每个 source 状态变化是否符合预期 | 把 source card 表现成独立自治 agent，越过真实能力边界 | 否 |
| T8 | 实现 Investigation Report 渲染 | report mock fixture、source findings | 调查完成后显示 risk、confidence、summary、evidence chain、recommended actions、limitations | 修改：`osint_agent_console_demo.html` 的 HTML/JS/CSS | T6, T7 | report 在运行前为 pending/placeholder；完成后内容完整；evidence chain 能对应 source findings | Run 完成后检查 report 字段；确认 evidence 与 source 内容一致 | report 写成泛泛 LLM 空话，缺少证据支撑 | 可与 T9 部分并行 |
| T9 | 实现 Agent Lab / Source Inspector | source detail mock fixture、source card click | 运行前 locked；运行后点击 source 可查看 raw result、normalized signals、reasoning notes、suggested action | 修改：`osint_agent_console_demo.html` 的 HTML/JS/CSS | T7 | 每个 source 可点击；右侧详情随选择变化；mock source boundary 清楚 | Run 前看 locked 状态；Run 后逐个点击 source card | Agent Lab 暗示真实多 agent 后端或真实 API 查询 | 可与 T8 部分并行 |
| T10 | 实现 simulated chat | chatResponses mock fixture、report/evidence 内容 | Chat 支持 blocking、false positive、confidence、next steps、evidence 等预设追问；未知问题有安全 fallback | 修改：`osint_agent_console_demo.html` 的 HTML/JS/CSS | T8 | Chat 明确标注 simulated/demo-only；回答基于页面已有 evidence；不声称真实 LLM | 输入支持问题和未知问题；检查回答是否越界 | 让观众误以为页面接入真实 LLM 或实时威胁情报 | 否 |
| T11 | 实现 Reset 完整复位 | 所有 UI 状态 | Reset 清空 log、source 状态、report、selected source、chat，并重新启用输入和 Run | 修改：`osint_agent_console_demo.html` 的 inline JS | T6, T7, T8, T9, T10 | Reset 后页面回到初始状态；Reset 后可再次 Run；旧 timeout 不继续污染新状态 | Run 到一半 Reset；Run 完成后 Reset；Reset 后再次 Run | 未清理 timer，导致旧流程继续写入 UI | 否 |
| T12 | 最终验收与视觉打磨 | Frontend SPEC acceptance criteria | 最终可演示 HTML 文件 | 修改：`osint_agent_console_demo.html` | T1-T11 | 所有 functional、boundary、visual acceptance criteria 通过；3 分钟内能讲清楚闭环 | 手动完整走查：打开、Run、source detail、chat、Reset、再次 Run；检查 console 无错误 | 演示流程能跑但边界不清，或视觉不像专业安全工具 | 否 |

## 5. Recommended Execution Order

1. T1 读取并锁定需求边界。
2. T2 创建单文件 HTML 基础骨架。
3. T3 搭建工作台布局。
4. T4 定义集中 mock 数据结构。
5. T5 渲染初始空状态。
6. T6 实现 Run Investigation 状态流程。
7. T7 实现 source cards 状态变化。
8. T8 实现 Investigation Report 渲染。
9. T9 实现 Agent Lab / Source Inspector。
10. T10 实现 simulated chat。
11. T11 实现 Reset 完整复位。
12. T12 最终验收与视觉打磨。

Parallel note:

- T3 和 T4 可以在 T2 后并行。
- T8 和 T9 可以在 T7 后部分并行。
- T10 建议在 T8 后执行，因为 chat 回答必须基于 report/evidence。
- T11 和 T12 必须最后做。

## 6. Suitable For One-Pass Completion

这些任务可以一次完成，完成后做简单检查即可：

- T1 读取并锁定需求边界。
- T2 创建单文件 HTML 基础骨架。
- T4 定义集中 mock 数据结构。
- T5 渲染初始空状态。

## 7. Tasks Requiring Stepwise Verification

这些任务必须分步验证，因为它们直接影响 demo 可信度和演示流程：

- T3 工作台布局：需要检查是否像安全分析工具，而不是 landing page。
- T6 Run Investigation 状态流程：需要检查运行中状态、重复点击、日志时序。
- T7 source cards 状态变化：需要检查每个 source 是否按预期变化。
- T8 report 渲染：需要检查 report 是否有证据支撑。
- T9 Agent Lab / Source Inspector：需要检查运行前 locked、运行后 source detail。
- T10 simulated chat：需要检查是否越界成真实 LLM 声称。
- T11 Reset：需要检查运行中 reset 和完成后 reset。
- T12 最终验收：需要完整走一遍演示路径。

## 8. Lightweight Guardrails

- 不要加后端。
- 不要加数据库。
- 不要加 npm / build tool。
- 不要真实请求外部 OSINT API。
- 不要假装 chat 是真实 LLM。
- 不要把 mock fixture 写成 confirmed backend contract。
- 不要做 landing page。
- 不要为了架构漂亮拆出多文件；当前交付物就是单文件 HTML。

