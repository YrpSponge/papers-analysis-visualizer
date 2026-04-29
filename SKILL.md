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
```/references/input_schema.md```

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
- interactive keywords/topics network
- topic trend chart area or section


### Optional static assets
- ```output/figures/keyword_network.png```
- ```output/figures/topic_trend.png```
- ```output/figures/paper_overview.png```

### Machine-readable output
- ```shared_data/analytics_summary.json```


---

## Core Functions

### 1. Paper Dashboard/Database View
Build a notion-like paper database/dashboard.

Each paper entry should display:

- clickable paper title
- recommendation index
- relevance score
- novelty score
- concise one-line summary
- keywords
- optional category / cluster label

Each entry should support interaction of:
- clicking and navigate to the paper through URL


The dashboard should support clear visual prioritization and quick scanning.

### 2. Recommendation Index
Generate a visual recommendation index for each paper.

This index must be derived only from available input fields such as:

- relevance score
- novelty score
- ranking position
- optional additional computed signals

The recommendation index may be shown as:

- score badge
- stars
- heat color
- other compact visual indicators

The computation should be simple, interpretable, and reproducible.

### 3. Keyword Network

Build an interactive keyword co-occurrence network.

Requirements:

- show the most central / hottest keywords
- clearly show the structure/correlation between keywords
- visually enlarge more important keywords
- support user zoom, drag, and pan
- allow clicking a keyword to inspect its related papers or topic trend
- keep labels concise and readable

This network must be constructed only from the provided keyword data.


### 4. Topic Trend View

Provide a topic-level trend view.

If historical data is available:

show publication or attention trend over time for a selected keyword/topic

If historical data is unavailable:

- show only current-batch distribution or topic presence
- do not claim a real temporal trend

Trend visualization should remain lightweight and visually clear.

---

## Style Requirements

- visual-first presentation: don't give too many complex literal presentation 
- dominant UI text should follow the user's most recent language (example: use Chinese UI text if the user prompts in Chinese)
- UI text should be concise and clear
- academic terms, paper keywords, and topic names must remain in original English wording
- avoid dense paragraphs
- prioritize charts, cards, badges, and compact labels over long narrative text
- the overall dashboard should support quick scanning and exploration

---

## Interaction Requirements

### 1. Paper interactions
- each paper entry must be clickable
- clicking a paper opens the original paper link

### 2. Keyword network interactions
- support zoom
- support drag
- support pan
- support hover or click for keyword inspection
- once clicking a keyword, switch the keyword bubble to center peek page to show its related papers and topic trend

### 3. Topic trend interactions
- clicking a keyword should update or reveal the corresponding topic trend section
- when possible, related papers under the selected topic should also be shown

---

## Language Policy

- overall interface language: Follow the user's most recent input language
- academic keywords, research topics, and paper terms: keep original wording
- paper titles: keep original wording
- concise UI labels may be written in Chinese

---

## Constraints

### Data constraints
- do not fabricate unsupported facts
- all displayed information must come directly from input fields or be computed from them
- do not introduce hidden metadata not present in the input

### Content constraints
- do not overload the page with large text blocks 
- do not output verbose paper-by-paper essays inside the dashboard
- do not translate academic terms such as CV, Agent, Skill into Chinese

### UX constraints
- keep text concise
- keep visual hierarchy clear
- prioritize readability and interactivity over - decorative complexity


---

## Failure/Fallback（后续有待改进）

If paper fields are missing:

- skip unsupported visual elements gracefully
- preserve the rest of the dashboard if possible

If historical data is missing:

- disable true time-series trend mode
- replace it with current topic distribution mode

If keyword data is too sparse:

- show a simplified keyword summary instead of a dense network

---

## Dependency



---

## Recommended Workflow