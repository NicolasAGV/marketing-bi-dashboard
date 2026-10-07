# Marketing BI Dashboard: Social Media Performance (Sep–Dec 2025)

An interactive 5-page dashboard built in Data Studio (Google) that follows one question: **what happens to a person who sees our videos, and was it worth the spend?**

**Dashboard:**  https://datastudio.google.com/reporting/650f844e-0f7f-4a54-af1c-2f31abe74276/page/p_epeab3o17d
**Author:** Nicolas Gonzalez Villagra · Data Analyst · [GitHub](https://github.com/NicolasAGV)

![Overview](images/overview.png)

---

## The story in 60 seconds

> We ran video content on Facebook, Pinterest and Snapchat for four months: 59.2M people reached, 74M impressions, about 800K invested.
>
> Overall, **Reach and engagement held steady**: Reach moved 3.95% between months and engagement rate 1.47%. But **attention did not**. The share of impressions that became a view fell from 13.5% in September to 8.4% in November, and recovered only slightly to 9.9% in December.
>
> Efficiency moved the same way. Cost per conversion rose from 45 to 72 in November, and ROAS fell from 0.65 to 0.41. These metrics move together; I can't prove one causes the other.
>
> By platform, there is a trade-off. **Pinterest wins attention and clicks** and has the best CPA and ROAS. **Snapchat wins interaction** (5.2% engagement) but is below average on attention and clicks, and is the least efficient. Retention is the same everywhere (about 70%).
>
> By content, **three videos (Rayo, Tiburon and Galaxia) are outliers**: double the attention (about 22% vs 9%) and double the click rate (about 1.1% vs 0.5%). In the underlying data they are also the only contents with ROAS above 1.
>
> So the next step is clear: find out what these three have in common, and make more of it.

**Latest movement (December vs the previous 31 days):** the dashboard opens on December with comparison arrows, and it shows a recovery. Attention (VTR) is up 17.6% and clicks (CTR) up 17.3%, while cost per conversion (CPA) is down 14.8% and ROAS is up 18.0%, with Spend and Reach almost flat. Even so, December stays below September's levels.

---

## The framework: from exposure to result

| Group | Metric | Question it answers | Formula |
|---|---|---|---|
| **Volume** | Reach | How many different people saw it? | Unique people |
| | Impressions | How many times was it shown? | Total displays, repeats included |
| | Views | How many times did someone watch it? | Impressions that became a view |
| | Frequency | How often did each person see it? | Impressions / Reach |
| **Funnel** | **Attention:** VTR | Did they stop to watch? | Views / Impressions |
| | **Retention:** VCR | Did they stay until the end? | Video completions / Views |
| | **Interaction:** ER | Did they react? | (Likes + comments + shares + saves) / Reach |
| | **Action:** CTR | Did they click? | Clicks / Impressions |
| **Cost** | Spend | How much did we invest? | Sum of ad spend |
| | CPM | What does 1,000 impressions cost? | Spend / Impressions × 1000 |
| | CPC | What does one click cost? | Spend / Clicks |
| | CPA | What does one conversion cost? | Spend / Conversions |
| | ROAS | How much revenue per unit spent? | Revenue / Spend |

All ratios are calculated as `SUM(a) / SUM(b)`, never as an average of row-level ratios.

---

## How to read the dashboard

- **Default view:** December 1–31, with arrows comparing against the previous period of equal length (Oct 31 – Nov 30).
- **Whole-period numbers** (used in the story above): set the date range to Sep 1 – Dec 31. Scorecards then show "No data" for the comparison, because there is no earlier period.

---

## Pages

| Page | Question | What it shows |
|---|---|---|
| **Overview** | How are we doing? | 8 KPI scorecards with date, content-group and platform filters |
| **Trend** | How does it evolve? | Reach, ER and VTR by month, with the max–min / average variation |
| **Platform** | Which platform is better? | VTR, VCR, ER and CTR by platform, against the overall average |
| **Content** | Which content stands out? | VTR by content with IQR bounds, and a table of all four funnel metrics with outliers highlighted |
| **Efficiency & ROI** | What does it cost, and does it pay back? | Spend, CPM, CPC, CPA and ROAS, by platform and by month |

---

## Method notes

- **Outliers** are detected with the IQR rule (1.5×) across the 20 contents, calculated in Python and entered in Data Studio as fixed values (the tool cannot compute percentiles over aggregated fields). They are labeled *non filtered*, because they stay the same when filters change.
- **Variation** in the Trend page is `(max − min) / average` of the monthly values.
- **Static annotations and insights** are written for the full dataset and labeled *non filtered*.
- **The Platform page has no platform filter**, so all three platforms are always visible for comparison.

## Data

A social-media dataset with 7,320 daily rows (Sep 1 – Dec 31, 2025), 3 platforms, 4 content groups and 20 contents. **Spend, conversions and revenue are synthetic**, so the efficiency findings (including ROAS below 1) demonstrate the analysis and are not real business results.

## Tools

Data Studio · Google Sheets · Python (pandas) for IQR bounds and variations

---

## Possible next steps

- Compare the three outlier videos against the rest (format, length, topic) to find what drives attention.
- Test whether the VTR decline is tied to content age (content decay).
- Add a spend-allocation scenario: how would the results change if budget moved toward Pinterest?
