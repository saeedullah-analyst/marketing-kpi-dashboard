# TechFuel Consulting — Social Media Performance Dashboard

Marketing analytics | Power BI | DAX | Star Schema | Multi-platform KPI tracking

---

This project builds a marketing analytics dashboard for TechFuel Consulting, an IT consulting brand running social media campaigns across LinkedIn, Instagram, and Facebook. The raw data consisted of separate platform logs — individual posts, engagement metrics, and follower counts across 2021 and 2022 — with no unified view across channels.

The three questions the dashboard was built to answer:

1. Are the 2021 and 2022 KPI targets being met?
2. Which platforms and content themes generate the strongest audience response?
3. Where are the gaps that need budget or strategy adjustments?

The full dashboard with visuals is in the PDF below.

**[View the Dashboard PDF](Project%202_Techfuel%20Consulting.pdf)**

---

## Technical Stack

| Layer | Tool / Method |
|---|---|
| BI Tool | Power BI Desktop |
| ETL | Power Query — multi-platform text ingestion, type casting, date parsing |
| Data Model | Star schema: interaction fact table linked to timeline, platform, and content theme dimensions |
| Calculations | DAX — total impressions, dynamic engagement rate (Engagement / Impressions), target achievement % |

---

## Data Model

```
         dim_platform
              │
dim_date ──► fact_interactions ◄── dim_content_theme
              │
         dim_target
```

Each row in `fact_interactions` represents one post. It connects to dimension tables for the platform it was published on, the content theme, the date, and the KPI targets set for that period.

---

## Dataset Overview

| Metric | 2021 | 2022 | Total |
|---|---|---|---|
| Total interactions | 3,479 | 1,102 | 4,581 |
| Total impressions | 55,909 | 22,050 | 77,959 |

---

## Key Findings

### Posting volume targets were largely missed in 2021

The organization set a target of 10 posts per platform per month. 2021 results:

| Platform | Target Achievement |
|---|---|
| LinkedIn | 90% |
| Instagram | 25% |
| Facebook | 12.5% |

By 2022, LinkedIn reached 100%. Instagram and Facebook both stabilised at 25% — an improvement for Facebook, flat for Instagram.

### LinkedIn outperforms on every engagement metric

| Platform | Avg Engagement Rate |
|---|---|
| LinkedIn | 5.88% |
| Instagram | 4.52% |
| Facebook | 0.66% |

LinkedIn regularly peaks at 10% during active campaign windows. Facebook never broke 2%, suggesting low organic reach regardless of posting frequency.

### Content theme performance varies significantly by platform

**LinkedIn:** Special Event and Employer Branding content drove the highest impressions. Special Event also held the highest engagement rate at 10% — the strongest single-theme result across all three platforms.

**Instagram:** Interview and Blogpost/News led on impressions, but Event and Special Event content generated the strongest actual engagement. The two metrics point in different directions, meaning reach and response are driven by different content types.

**Facebook:** Interview content produced high impressions but collapsed to 0% engagement — reach with no response. Scholarship and Testimonial themes generated the highest engagement rates despite lower impression volumes.

### Follower growth vs. targets

| Platform | Target | Actual | Variance |
|---|---|---|---|
| Instagram | 600 | 874 (Apr 2022) | +45.7% |
| LinkedIn | 1,432 | 1,451 (Apr 2022) | +1.3% |
| Facebook | 1,712 | 1,668 (Dec 2021) | -2.6% |

Instagram significantly exceeded its target. LinkedIn tracked closely. Facebook missed — the only platform to fall below its follower target, consistent with its low engagement numbers throughout the analysis period.

---

## DAX Measures

```
// Total impressions
Total Impressions = SUM(fact_interactions[impressions])

// Engagement rate
Engagement Rate =
DIVIDE(
    SUM(fact_interactions[engagements]),
    SUM(fact_interactions[impressions]),
    0
)

// Target achievement percentage
Target Achievement % =
DIVIDE(
    [Total Posts],
    [Monthly Post Target],
    0
)
```

---

## Project Impact

| Finding | Recommended Action |
|---|---|
| Facebook engagement at 0.66% | Reduce posting frequency, reallocate budget |
| Interview content: high reach, 0% engagement on Facebook | Stop format on Facebook |
| Special Event content: 10% engagement on LinkedIn | Prioritise for LinkedIn calendar |
| Instagram follower target exceeded by 45% | Maintain current content mix |
| Manual tracking lists across platforms | Replaced with unified live dashboard |

---
