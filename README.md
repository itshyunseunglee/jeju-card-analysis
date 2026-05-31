# Jeju Card Spending Analysis

📊 [View Notebook 1 on nbviewer](https://nbviewer.org/github/itshyunseunglee/jeju-card-analysis/blob/main/jeju_analysis1.ipynb) — Spending Trends by Age, Season, and User Type

📊 [View Notebook 2 on nbviewer](https://nbviewer.org/github/itshyunseunglee/jeju-card-analysis/blob/main/jeju_analysis2.ipynb) — Region-Level Analysis + Café vs. Visitor Population

Analyzed card transaction data from Jeju Island (2017–2018) to figure out spending trends by age, season, region, and industry. The overall goal was to see whether the data supports opening a café franchise in Jeju and, if so, where and when.

## Datasets

| File | Description |
|------|-------------|
| `data/jeju_card.csv` | Card spending by year/month, user type, age group, gender, and industry. 19,573 rows. |
| `data/jeju_card_region_2017.csv` | Region-level card spending data for 2017. 26,968 rows. |
| `data/jeju_card_region_2018.csv` | Region-level card spending data for 2018. 27,183 rows. |
| `data/jeju_population.csv` | Daily visitor population by region, gender, and age group. 527,026 rows. |

## Notebooks

### `jeju_analysis1.ipynb` — Spending Trends by Age, Season, and User Type

**Preprocessing**
- Dropped incomplete 2016 data (only Sep–Dec available)
- Fixed inconsistent label: `'20 미만'` → `'20대미만'`
- Dropped the `'기타'` industry — it only existed in 2017, making year-over-year comparison unreliable
- Ordered age group column using `pd.Categorical` for consistent chart ordering

**Analysis**
- Monthly spending trends across 2017–2018
- Spending comparison by age group and year
- Residents vs. domestic tourists comparison
- Industry breakdown by year

**Findings**
- Spending peaks in July–August and drops heading into winter
- Overall spending declined in 2018 vs. 2017 across all groups
- 20s–40s make up the largest share of card users
- Spending per person increases with age — 60s+ have the highest per-person spend
- 40s have the highest total spending volume
- Shopping and food & beverage dominate across all age groups

### `jeju_analysis2.ipynb` — Region-Level Analysis + Café vs. Visitor Population

**Preprocessing**
- Merged 2017 and 2018 region datasets after removing industry categories that only appeared in one year (`기타 갬블링 및 베팅업`, `택시 운송업`)
- Dropped `버스 운송업` — only 5 total customers, which skewed the per-person spending metric
- Reformatted date column from `20170101` to `2017-01` to align with the card dataset
- Added `'성'` suffix to gender values in the population dataset before merging

**Analysis**
- Top industries ranked by total sales, total customers, and spending per customer
- Top regions ranked by total sales, total customers, and spending per customer
- Joined card data with visitor population data by month, district, and gender
- Focused on `비알콜 음료점업` (cafés) specifically

**Findings**
- Korean restaurants (#1 in total sales), convenience stores (#1 in customer count)
- Bars/pubs had by far the highest spending per customer
- Yeondong (연동) had the highest total sales; Nohyeong-dong (노형동) had the most customers
- Top 5 regions by per-person spending: Yeraedong, Yeongcheondong, Yongdam2-dong, Yeondong, Ildo1-dong
- Café sales had a clear positive correlation with visitor population (r ≈ 0.633)
- No such correlation across all industries combined (r ≈ 0.163), suggesting cafés are particularly traffic-sensitive

## Conclusion

Based on the card data, the best strategy for a café entry into Jeju would be:
- **Target audience**: 30s–40s
- **Timing**: Open before or at the start of summer (June–August peak)
- **Location**: High-traffic tourist areas like Yeondong or Yongdam2-dong, where visitor population and café revenue are closely linked

## Stack

Python, pandas, matplotlib, seaborn

## Structure

```
Jeju_project/
├── data/
│   ├── jeju_card.csv
│   ├── jeju_card_region_2017.csv
│   ├── jeju_card_region_2018.csv
│   └── jeju_population.csv
├── jeju_analysis1.ipynb
├── jeju_analysis2.ipynb
└── README.md
```
