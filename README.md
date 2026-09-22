# aikeda-data-analysis

把数据集、工作簿、数据库导出或参考报告转化为一套可重复执行的经营分析交付流程。

该 Skill 覆盖数据质量检查、指标口径、经营分析、可编辑图表、交互式仪表盘与飞书报告，并要求关键结论可追溯到原始数据、计算过程和可验证的图表证据。仪表盘默认采用组件化单页数据应用，而不是互不联动的静态图表集合。

## 功能亮点

- **质量先行** — 识别重复、缺失、孤儿键、异常日期和口径风险，并给出分析准入结论。
- **指标可复现** — 明确公式、分子、分母、粒度、时间窗口、筛选和数据来源。
- **结论可下钻** — 从整体结果进入时间、地区、产品、渠道、客群或 cohort 等解释维度。
- **交互式仪表盘** — 支持共享筛选状态、动态重算、异常状态、数据追溯与浏览器验收。
- **证据化报告** — 将结论、图表证据、限制和行动建议组织为可验证的飞书文档。

## 安装

将仓库克隆到你所使用的 Agent 的 Skill 目录：

```bash
git clone https://github.com/aikeda-ai/aikeda-data-analysis.git <skills-directory>/aikeda-data-analysis
```

确保运行环境能够读取目录中的 `SKILL.md`，并支持 Skill 所需的数据处理、浏览器验收和文档发布能力。

## 使用方式

在任务中引用 `aikeda-data-analysis`，同时提供数据源、业务问题、分析周期和期望产出。例如：

```text
请使用 aikeda-data-analysis 分析这份经营数据。
先完成数据质量检查和指标口径，再生成可交互仪表盘，
最后分别产出数据质量与指标口径、完整经营分析两份飞书文档。
```

用户可以指定停止点，例如只生成演示数据、只做质量检查、只制作仪表盘，或只更新报告。

## 文件结构

```text
aikeda-data-analysis/
├── SKILL.md
└── references/
    └── deliverable-contract.md
```

- `SKILL.md`：入口、适用场景、分析流程和核心约束。
- `references/deliverable-contract.md`：报告、图表、仪表盘、飞书发布和最终验收标准。

## 工作流程

```text
业务问题与数据
      ↓
分析范围与数据质量检查
      ↓
指标定义与口径确认
      ↓
整体分析与多维下钻
      ↓
可编辑图表与交互式仪表盘
      ↓
飞书报告、追溯信息与最终验收
```

## License

MIT

<!-- AUTO-README-START -->

## Auto-generated Project Map

- Project: `aikeda-data-analysis`

This block is managed by `update-readme` and can be regenerated at any time.

<!-- AUTO-README-END -->
