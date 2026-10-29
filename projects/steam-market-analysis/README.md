# Steam Market & Product Analysis

> Public source snapshot: the two notebooks are provided with saved outputs and local metadata removed. Their analytical code is unchanged. They have not been rerun end to end for this publication. The original CSV, processed data, practice exercises and PBIX files are not distributed. The SQL folder is currently empty; the PostgreSQL queries/views required to reproduce the report are not yet included.

[Portfolio](https://jinniehoho.github.io/) · [Report (English PDF)](../../reports/steam-report.pdf) · [Notebooks](notebooks/) · [Data model](docs/data_model.md)


## Overview

This project analyzes the Steam PC game market from the perspective of a small indie game studio preparing a new game concept.

The goal is not to identify a single "best" genre, but to examine how market supply, observed player traction, user response, pricing, and recent market trends differ across game segments.

The analysis ultimately narrows the market into candidate segments that may be worth further product investigation.

---

## Business Context

### Stakeholder

Product / Business Lead at a small indie game studio.

### Business Goal

Support early-stage product planning by answering questions such as:

- Which genres have high market supply and strong competitive pressure?
- Which genres show relatively strong player traction?
- How do user satisfaction and engagement differ across game characteristics?
- How does pricing relate to traction and satisfaction?
- How has genre presence changed over time?
- Are there segments with relatively low supply but promising traction that may deserve further investigation?

The analysis is intended to support product exploration rather than predict commercial success.

---

## Dataset

**Steam Games Dataset – FronkonGames**

Source:
- Hugging Face
- Steam API
- SteamSpy

The dataset contains information on Steam games including:

- Release date
- Price
- Estimated owners
- Peak CCU
- Positive and negative reviews
- Recommendations
- Average and median playtime
- Genres
- Categories
- Tags
- Developers and publishers
- Platform support
- Metacritic and user scores

The raw dataset is stored separately and is not modified during the analysis process.

---

## Important Data Interpretation

The dataset does not contain actual sales or revenue.

Therefore:

- `Estimated owners` is treated as an ownership / traction proxy, not actual sales.
- `Peak CCU` is treated as an activity / traction indicator, not total player count.
- Review volume is not treated as user satisfaction by itself.
- Playtime is interpreted as engagement, not automatically as satisfaction.
- Relationships found in the data are descriptive associations and are not interpreted as causal effects.
- Candidate market segments are treated as areas for further investigation, not guaranteed business opportunities.

---

## Analytical Framework

The project follows the analytical flow:

**Supply / Competition  
→ Demand / Traction  
→ Satisfaction & Engagement  
→ Pricing  
→ Market Trend  
→ Candidate Segments**

### 1. Market Supply / Competition

**Question**

Which genres have the highest market supply, and how does recent release activity differ across genres?

Main dimensions and metrics:

- Genre
- Number of games
- Recent releases
- Release period

This stage describes supply concentration rather than assuming that a high number of games automatically means poor market attractiveness.

---

### 2. Demand / Traction

**Question**

Which genres show relatively strong observed player traction?

Possible traction indicators include:

- Estimated owners
- Peak CCU
- Recommendations
- Review volume

Both total market traction and typical traction per game are considered where appropriate to avoid automatically favoring genres with a large number of titles.

---

### 3. Satisfaction & Engagement

**Question**

How do user satisfaction and engagement differ across genres and game characteristics?

Satisfaction indicators may include:

- Positive review ratio
- User score
- Recommendations

Engagement indicators include:

- Average playtime
- Median playtime

Genres, categories, and selected tags are used as comparison dimensions.

Satisfaction and engagement are treated as separate concepts.

---

### 4. Pricing

**Question**

How do player traction and satisfaction differ across price segments?

The analysis compares price bands with:

- Traction indicators
- Satisfaction indicators
- Engagement indicators where relevant

Free-to-play titles are separated where necessary because their market structure differs substantially from paid games.

---

### 5. Market Trends

**Question**

How has genre presence and observed traction changed over time?

Release dates are used to examine:

- Changes in genre coverage
- Recent release activity
- Relative market presence over time

Changes in genre coverage are interpreted as changes in market presence, not automatically as market growth.

---

### 6. Candidate Segment Analysis

The final stage combines previous findings rather than using a single standalone metric.

Potential candidate segments are identified by comparing:

- Supply intensity
- Observed traction
- Satisfaction
- Engagement
- Recent market presence

The purpose is to identify segments that may deserve deeper investigation.

These results are not interpreted as evidence of guaranteed commercial opportunity.

---

## Data Preparation Principles

The project follows the principle:

> **No cleaning without analytical reason.**

Values are not removed or transformed simply because they appear unusual.

Each issue is evaluated according to:

1. What the value represents
2. Whether it affects a business question
3. Whether it is a genuine data-quality problem
4. Whether transformation would change its original meaning

The processing workflow follows:

**Raw  
→ Audit  
→ Decision  
→ Clean / Transform  
→ Validate  
→ Processed**

The original raw dataset remains unchanged.

---

## Data Audit

Data-quality checks include:

- Dataset dimensions
- Data types
- Missing values
- Zero values
- Duplicate records
- Unusual values
- Multi-value categorical columns
- Numeric distributions
- Release-date coverage
- Estimated-owner ranges

Audit decisions are documented using the structure:

| Column | Issue Observed | Business Relevance | Decision | Reason |
|---|---|---|---|---|
| Example | Example issue | Related business question | Keep / Transform / Exclude | Analytical justification |

---

## Technology Stack

### Python / Pandas

Used for:

- Data inspection
- Data auditing
- Cleaning
- Transformation
- Feature creation
- Exploratory analysis
- Validation

### PostgreSQL

Used for:

- Structured analytical data storage
- SQL aggregation
- Reusable analytical queries
- Preparing datasets for Power BI

### Power BI

Used for:

- Interactive reporting
- KPI visualization
- Market comparison
- Trend analysis
- Final decision-support dashboard

### Excel

Used selectively for planning, documentation, and intermediate checks.

---

## Power BI Report

The final Power BI report is organized into six pages.

### 1. Market Overview

Provides a high-level view of the Steam market and genre supply.

### 2. Supply vs Traction

Compares market supply with observed player traction to identify contrasting market positions.

### 3. Response & Pricing

Examines satisfaction, engagement, and performance across price segments.

### 4. Market Trends

Shows changes in relative genre coverage and market presence over time.

### 5. Market Entry

Combines major analytical results to narrow the market into candidate segments.

### 6. Candidate Deep Dive

Provides a closer look at selected candidate genres and supporting product signals.

The final page is intended as a decision-support summary rather than a prediction of commercial success.

---

## Example Analytical Interpretation

The final analysis focuses on identifying segments where multiple signals align.

For example, a candidate segment may show:

- Relatively moderate supply
- Above-benchmark traction
- Stable or increasing recent market presence
- Supportive user-response indicators

These signals are interpreted together rather than relying on a single metric.

The analysis also considers product-level characteristics such as selected categories or features when examining candidate segments.

---

## Limitations

Several limitations should be considered when interpreting the results.

### No actual sales or revenue data

The dataset does not provide verified unit sales or revenue.

Estimated ownership and activity measures therefore serve only as proxies.

### Ownership estimates

`Estimated owners` values are estimates and may contain broad ownership ranges.

They should not be interpreted as exact sales figures.

### Historical accumulation

Older games have had more time to accumulate owners, reviews, recommendations, and playtime.

Release period therefore needs to be considered when comparing titles.

### Genre overlap

Steam games can belong to multiple genres, categories, and tags.

Aggregated genre-level results are therefore not mutually exclusive.

### Missing and uneven data coverage

Some fields, such as external review scores, are only available for part of the dataset.

These variables are not assumed to represent the entire Steam market.

### Observational analysis

The project identifies associations in historical Steam data.

It does not establish causal relationships between game characteristics and commercial performance.

### Business factors outside the dataset

The dataset does not include several factors that strongly influence game performance, such as:

- Development budget
- Marketing spend
- Studio reputation
- Brand awareness
- Production quality
- Development difficulty
- Team capability
- External distribution

Candidate segments should therefore be evaluated alongside production scope and studio capabilities.

---

## Project Structure

- `README.md`
- `README_DE.md`
- `data/raw/` (local only, not published)
- `data/processed/` (local only, not published)
- `notebooks/`
- `sql/` (not included; original folder currently empty)
- [Report PDF](../../reports/steam-report.pdf)
- `docs/`

The raw dataset is intentionally kept separate from processed analytical data.

---
## How to View the Project

### Power BI

Open the [English PDF report](../../reports/steam-report.pdf). The PBIX is retained locally.

A PDF export of the report is also included for quick review.

### Python

The notebooks document the workflow from:

- Data inspection
- Data audit
- Data cleaning
- Transformation
- Validation
- Analysis preparation

### SQL

The local report connects to PostgreSQL views. Their SQL definitions are not included in this public snapshot, so the full pipeline cannot yet be reproduced from these files alone.

---

## Power BI Data Refresh

The Power BI report contains the imported analytical model.

Data refresh may require reconfiguration of the original PostgreSQL or local data-source connection because local connection paths and credentials are environment-specific.

The existing report can still be reviewed without refreshing the source data.

---

## Project Objective

This project is designed as both an analytical case study and a portfolio project.

The intended workflow is shown below. The public snapshot does not yet reproduce the SQL and report stages:

**Data Acquisition**  
→ **Data Understanding**  
→ **Data Audit**  
→ **Data Preparation**  
→ **SQL Analysis**  
→ **Data Modeling**  
→ **Business Intelligence**  
→ **Interpretation**

The emphasis is not only on producing visualizations, but on connecting data preparation and analytical decisions to a defined business problem.