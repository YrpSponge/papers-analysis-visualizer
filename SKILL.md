---
name: papers-analysis-visualizer
description: >
  Build a research dashboard and visual analytics summary from structured paper data, focusing on paper recommendation, keyword network visualization and topic trend exploration.
author: RuipengYu
version: 1.0.0

---

# Paper Analysis Visualizer

## Purpose

Use this skill to transform a ranked paper list into two interactive visualization modules:
1. An interactive research database/dashboard for organized paper collection and convenient human browsing;
2. Interactive visualizations of macro information, including topic structures, keywords correlations and trends of certain topics.

This skill focuses on:
- collecting papers and corresponding information from certain sources(这里是不是应该明确一下从哪里获取什么？)
- presenting papers in a notion-like database/dashboard format
- highlighting recommended papers with concise, visual-first signals
- showing keyword/topic structure through an interactive keyword network
- showing topic-level trends when historical data is available

This skill is designed for users who want to quickly understand:
- which papers are most worth reading in user's interested direction
- what is the key takeaway of each paper
- what topics are currently the hottest
- which keywords are central or potentially emerging
- how these keywords/topics correlate with others
- how a topic evolves over time 

---

## Use this skill when

Use this skill when the user asks for any of the following (or similar request):

- a collection of recommended papers
- a paper dashboard
- a notion-like paper database
- an interactive paper browser
- keyword network visualization
- topic hotspot overview
- topic trend analysis
- a visual summary of ranked papers
- a clickable interface for browsing paper results

Typical requests include:
- “帮我整理这些paper”
- “帮我把这些 paper 做成一个 dashboard”
- “给我一个像 Notion database 一样的论文整理页”
- “展示关键词网络和热点主题”
- “整理这个主题/关键词相关的主题/关键词”
- “点开关键词后可以看趋势”
- “把这些论文整理做成可交互可浏览的图形界面”

---

## Do not use this skill for

Do not use this skill for:
- fetching papers from arXiv
- ranking papers from scratch
- generating paper summaries from raw abstracts
- writing the final daily report narrative
- making claims with hallucinations that require information not present in the input data

This skill does **not**:
- infer facts not supported by the input sources
- perform deep full-paper analysis
- fabricate author relations, topic evolution, or novelty claims
- translate academic keywords such as CV, Agent, Skill into Chinese

---

## Inputs

### Required Inputs

Input must include a ranked paper list.

Each paper entry should contain at least the following information:
- 'title'
- 'url'
- 'authors'
- 'relevance_score'
- 'novelty_score'
- 'one_line_summary'
- 'keywords'

Recommended additional fields:
- 'paper_id'
- 'published_date'
- 'category'
- 'community_label'

Example input schema: 
'/references/input_schema.md'

### Optional Inputs

Historical data may be provided for real trend analysis.

Accepted optional historical inputs include:
- archived paper lists from previous days/weeks
- keyword frequency time series
- topic-level daily/weekly counts

If historical data is not available:
- trend charts must fall back to current-batch topic distribution only
- “emerging keywords” must be treated as heuristic candidates rather than factual trend claims

## Outputs

### Main outputs: 
```output/paper_analysis_visualization.html``` containing:
- interactive paper database/dashboard view
- each paper
- interactive keyword network
- topic trend chart area or section

## Reasoning Flow

## Tools Table

## Docs Table

## Output Rules