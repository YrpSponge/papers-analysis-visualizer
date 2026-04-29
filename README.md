# Papers Analysis Visualizer

将结构化论文分析结果转化为交互式可视化仪表盘的 agent skill。

## 功能概述

输入：排好序的论文列表，每篇附带 relevance/novelty 评分、一句话总结、关键词等信息。

输出：一个自包含的 HTML 交互式仪表盘，包含三种联动视图：

| 视图 | 说明 |
|------|------|
| 论文库仪表盘 | Notion 风格表格/卡片，展示推荐指数、关键词标签、一句话概括，可搜索过滤、点击查看详情 |
| 关键词共现网络 | 力导向图，节点大小=频次，连线=共现关系，区分热点主题与新兴关键词，支持拖拽缩放 |
| 话题趋势图 | 折线/柱状图，点击关键词网络节点后展示该主题的历年论文趋势 |

技术路线：Python 3.11+（jinja2 + 标准库）做数据处理管线，ECharts 5.5+（CDN）做前端可视化，输出为浏览器直接可打开的单一 HTML 文件。

---

## 开发阶段

### 阶段一：初始化与设计 ✅

- [x] 项目骨架搭建（目录结构、文件占位）
- [x] CLAUDE.md — Claude Code 协作指南
- [x] SKILL.md — Skill 功能定义（输入/输出/核心功能/交互/约束）
- [x] `references/input_schema.md` — 输入数据格式样例

### 阶段二：核心实现 🚧

- [ ] `references/output_schema.md` — 输出格式详细说明
- [ ] `references/visualization_rules.md` — 可视化设计细则
- [ ] `scripts/utils.py` — 共享工具（JSON 加载、schema 校验、归一化）
- [ ] `scripts/compute_analytics.py` — 衍生数据计算（关键词频次、共现矩阵、逐年趋势、推荐指数）
- [ ] `scripts/build_dashboard.py` — HTML 生成（jinja2 模板渲染、ECharts 配置嵌入）
- [ ] `scripts/run_visualizer.py` — 管线入口（CLI 参数解析、编排 compute → build）
- [ ] `assets/dashboard_template.html` — Jinja2 HTML 骨架模板
- [ ] `assets/style.css` — 仪表盘样式

### 阶段三：测试

- [ ] `tests/fixtures/summarized_papers_sample.json` — 测试用样例论文数据
- [ ] `tests/test_compute_analytics.py` — 计算逻辑单元测试
- [ ] `tests/test_build_dashboard.py` — HTML 生成测试
- [ ] 路由测试 — 验证 LLM 在正确场景/边界内调用本 skill
- [ ] 系统联调 — WorkBuddy 中端到端跑通（上游输入 → 本 skill → 下游渲染）

### 阶段四：完善与优化

- [ ] 配色方案确定（当前 ECharts 默认配色）
- [ ] Failure/Fallback 逻辑（缺字段降级、数据稀疏简化视图）
- [ ] 静态资源导出（关键词网络截图、趋势图 PNG）
- [ ] 移动端响应式适配
- [ ] 更多输入格式支持（CSV、BibTeX）

---

## 项目结构

```
papers-analysis-visualizer/
├── CLAUDE.md                     # Claude Code 协作指南
├── SKILL.md                      # Skill 定义（agent 系统读取）
├── README.md                     # 本文件
├── scripts/                      # Python 源码
│   ├── run_visualizer.py         # 管线入口
│   ├── compute_analytics.py      # 衍生数据计算
│   ├── build_dashboard.py        # HTML 生成
│   └── utils.py                  # 共享工具
├── assets/                       # 前端资源
│   ├── dashboard_template.html   # Jinja2 HTML 骨架
│   └── style.css                 # 仪表盘样式
├── references/                   # 设计规范文档
│   ├── input_schema.md           # 输入格式
│   ├── output_schema.md          # 输出格式
│   └── visualization_rules.md    # 可视化细则
├── data/                         # 运行时输入数据
├── output/                       # 生成的 HTML
└── tests/                        # 测试
    ├── test_compute_analytics.py
    ├── test_build_dashboard.py
    └── fixtures/
        └── summarized_papers_sample.json
```

---

## 协作说明

- 对话语言：中文
- 代码：Python（PEP 8 + type hints），JavaScript（camelCase，嵌入 HTML）
- 学术术语不翻译（Agent、Skill、CV 等保持原文）
