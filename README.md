# Knowledge Flow on Stack Overflow — The AI Effect (2022–2024)
### COSC 2671 — Social Media and Network Analysis | Assignment 2 | Group 51

---

## Research Question
How has the emergence of AI coding assistants (ChatGPT, GPT-4, GitHub Copilot) impacted knowledge flow, community structure, and answer quality on Stack Overflow between 2022 and 2024? And who are the most influential human knowledge brokers that persisted through this transition?

---

## Team Members
| Name | Student ID |
|------|-----------|
| Ritam Basu | sXXXXXXX |
| Yutika Rayate | s4106671 |

---

## Repository Contents

| File | Description |
|------|-------------|
| `s4106671_PG_51.ipynb` | Main analysis notebook — single file, run top to bottom |
| `data_sample_Group51.csv` | Representative data sample (1,500 rows, 500 per year) |
| `Report_SNMA_Group51_Blue.pdf` | Final report |
| `Worksheet_SNMA_Group51.pdf` | Team worksheet, timesheets, self-reflections |

---

## ▶ How to Run — Step by Step

### Step 1 — Install Required Packages

All required packages are automatically installed in the first cell of the notebook. Alternatively, install manually:

```bash
pip install pandas numpy networkx scikit-learn vaderSentiment python-louvain matplotlib seaborn
```

| Package | Version Tested | Purpose |
|---------|---------------|---------|
| pandas | ≥1.5 | Data loading and manipulation |
| numpy | ≥1.23 | Numerical operations |
| networkx | ≥2.8 | Graph construction, PageRank, Betweenness |
| scikit-learn | ≥1.1 | LDA topic modelling, CountVectorizer |
| vaderSentiment | ≥3.3 | Sentiment analysis |
| python-louvain | ≥0.16 | Louvain community detection |
| matplotlib | ≥3.6 | All figures and visualisations |
| seaborn | ≥0.12 | Plot styling |

---

### Step 2 — Prepare Input Files

The notebook expects the following files **in the same directory** as the notebook:

```
SMNA/
├── s4106671_PG_51.ipynb       ← notebook
├── answers_2022.csv            ← required (50,000 rows)
├── answers_2023.csv            ← required (50,000 rows)
└── answers_2024.csv            ← required (50,000 rows)
```

**Expected input columns (all three CSVs must have these):**

| Column | Type | Description |
|--------|------|-------------|
| `answer_id` | int | Unique answer identifier |
| `question_id` | int | Associated question ID |
| `answerer_user_id` | int | User ID of the answerer |
| `asker_user_id` | int | User ID of the question asker |
| `answer_date` | datetime | Timestamp of the answer |
| `answer_score` | int | Community upvote score |
| `is_accepted` | int | 1 = accepted answer, 0 = not accepted |
| `answer_body` | str | Raw HTML content of the answer |
| `comment_count` | int | Number of comments |
| `question_title` | str | Title of the parent question |

> **Dataset Note:** The full CSV files (~183 MB total) exceed GitHub's file size limit and are not included in this repository. A representative sample (`data_sample_Group51.csv`, 1,500 rows) is provided to show the data structure. The full dataset is available from the Stack Overflow public archive:
> https://archive.org/details/stackexchange

---

### Step 3 — Run Order

**There is only one file to run:** `s4106671_PG_51.ipynb`

Run all cells **top to bottom in order**. Do not skip sections — each section depends on outputs from the previous one.

| Section | Contents | Depends On |
|---------|----------|------------|
| Section 0 | Imports & package installation | Nothing |
| Section 1 | Data loading & EDA | Section 0 |
| Section 2 | Text pre-processing (clean_lda, clean_vader) | Section 1 |
| Section 3 | Network construction (DiGraph) | Section 1 |
| Section 4 | Centrality — PageRank, Betweenness | Section 3 |
| Section 5 | Community detection (Louvain) | Section 3 |
| Section 6 | Temporal analysis + AI period comparison | Section 1, 2 |
| Section 7 | LDA topic modelling | Section 2 |
| Section 8 | VADER sentiment analysis | Section 2 |
| Section 9 | Integration — brokers vs average users | Section 4, 7, 8 |
| Section 6b | AI impact figures (topic decline) | Section 6, 7 |
| Final | Success criteria summary (SC1–SC5) | All sections |

---

### Step 4 — Expected Outputs

All figures are saved automatically to an `outputs/` folder created in the same directory:

| Figure File | Description |
|-------------|-------------|
| `fig01_dataset_overview.png` | Answers per year, acceptance rate, avg score |
| `fig02_top10_brokers.png` | Top-10 PageRank + acceptance rate |
| `fig03_degree_distributions.png` | In/out-degree distributions |
| `fig04_indeg_outdeg_scatter.png` | In vs out degree scatter |
| `fig05_community_analysis.png` | Community sizes + role ratios |
| `fig06_temporal_ai.png` | Monthly volume + acceptance rate with AI milestones |
| `fig07_topic_decline.png` | Monthly volume by topic |
| `fig08_period_comparison.png` | Pre/Post AI period metrics |
| `fig09_lda_topic_words.png` | Top-10 words per LDA topic |
| `fig10_topic_analysis.png` | Topic distribution + acceptance by topic |
| `fig11_sentiment_analysis.png` | VADER sentiment 4-panel |
| `fig12_integration_comparison.png` | Brokers vs average users |
| `fig13_topic_specialisation.png` | Topic specialisation comparison |
| `fig15_topic_decline_rate.png` | Topic decline rate bar chart |

---

## Security & Credentials

> ⚠️ This repository contains **no API keys, access tokens, passwords, or private credentials** of any kind.
>
> The dataset used is fully public (Stack Overflow CC BY-SA 4.0). No authentication is required to access or reproduce this analysis.

---

## Methods Summary

| Method | Tool | Purpose | SC |
|--------|------|---------|-----|
| Temporal Analysis | pandas | Volume change pre/post AI | SC1 |
| LDA Topic Modelling | scikit-learn | Topic-specific decline | SC2 |
| PageRank (α=0.85) | networkx | Identify knowledge brokers | SC3, SC4 |
| Betweenness Centrality | networkx | Bridge users between communities | SC3 |
| Louvain Community Detection | python-louvain | Community structure | SC3 |
| VADER Sentiment | vaderSentiment | Answer quality measurement | SC4, SC5 |

---

## Key Results

| Criterion | Finding |
|-----------|---------|
| SC1 | Volume fell 70%: 15,378 → 4,545 answers/month (pre-ChatGPT → GPT-4+ era) |
| SC2 | Numerical & Arrays fell fastest (−76%); Data Processing & APIs slowest (−62%) |
| SC3 | 689 communities detected; top-20 broker positions volatile year-over-year |
| SC4 | Top-10 brokers: 53.7% acceptance rate vs 25.9% platform average |
| SC5 | Accepted answers VADER: 0.227 vs non-accepted: 0.210; sentiment stable post-AI |

---

## AI Milestones

| Date | Event |
|------|-------|
| Nov 30, 2022 | ChatGPT public launch |
| Mar 14, 2023 | GPT-4 + Claude 1.0 release |
| Dec 19, 2023 | GitHub Copilot Enterprise GA |

---

## License
- Dataset: Stack Overflow public archive — CC BY-SA 4.0
- Code: Academic use only — COSC 2671 Assignment 2, RMIT University, Semester 1 2026
