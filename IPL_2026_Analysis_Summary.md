# 🏏 IPL 2026 — Deliveries Data Analysis Summary

> **Notebook:** `IPL_2026_Analysis.ipynb`
> **Dataset:** `ipl_2026_deliveries.csv`
>**Tools Used:** Python · Pandas · NumPy · Matplotlib · Seaborn

---

## 📋 Table of Contents

1. [Dataset Overview](#1-dataset-overview)
2. [Feature Engineering](#2-feature-engineering)
3. [Batting Analysis (Team-Level)](#3-batting-analysis-team-level)
4. [Batsmen Analysis (Player-Level)](#4-batsmen-analysis-player-level)
5. [Bowler Analysis](#5-bowler-analysis)
6. [Wicket Type Breakdown](#6-wicket-type-breakdown)
7. [Over-by-Over Analysis](#7-over-by-over-analysis)
8. [Phase-wise Run Scoring by Team](#8-phase-wise-run-scoring-by-team)

---

## 1. Dataset Overview

### Shape & Structure

| Property | Value |
|---|---|
| Total rows (deliveries) | **17,477** |
| Total columns | **21** |
| Season | 2026 |
| Total matches | **74** |
| Total teams | **10** |

### Columns

```
match_id, season, phase, match_no, date, venue, batting_team, bowling_team,
innings, over, striker, bowler, runs_of_bat, extras, wide, legbyes,
byes, noballs, wicket_type, player_dismissed, fielder
```

### Teams Participating

`SRH`, `RCB`, `KKR`, `MI`, `CSK`, `RR`, `GT`, `PBKS`, `LSG`, `DC`

### Missing Values

Only three columns had null values: `wicket_type`, `player_dismissed`, and `fielder` — which is expected, as they are only populated when a wicket falls.

### Tournament Phases

The dataset covers the full tournament: **Group Stage → Playoffs → Final**

The final (match 74, `202674`) was played on **May 31, 2026** at **Narendra Modi Stadium, Ahmedabad** between **RCB** and **GT**.

---

## 2. Feature Engineering

Four new columns were engineered from the raw data:

| New Column | Logic | Purpose |
|---|---|---|
| `total_runs` | `runs_of_bat + extras` | Total runs per delivery |
| `is_six` | `1` if `runs_of_bat == 6`, else `0` | Flag sixes |
| `is_four` | `1` if `runs_of_bat == 4`, else `0` | Flag fours |
| `is_wicket` | `1` if `wicket_type` is not null, else `0` | Flag wicket deliveries |
| `phase_group` | Function on `over` value | Categorise over into game phase |

---

## 3. Batting Analysis (Team-Level)

### 3.1 Most Runs Scored by a Team

Teams ranked by total runs scored across the tournament:

| Rank | Team | Total Runs |
|---|---|---|
| 1 | GT | 3,083 |
| 2 | RR | 3,071 |
| 3 | RCB | 3,054 |
| 4 | SRH | 3,041 |
| 5 | PBKS | 2,704 |

> Visualised as a bar chart with value annotations on each bar.

### 3.2 Boundary Hitting by Team (Fours & Sixes)

| Team | Sixes | Fours | Total Boundaries |
|---|---|---|---|
| CSK | 124 | 220 | 344 |
| DC | 117 | 225 | 342 |
| **GT** | **124** | **292** | **416** |
| KKR | 115 | 192 | 307 |
| LSG | 127 | 208 | 335 |

> GT scored the most boundaries overall (416), driven heavily by their fours count (292).
> Visualised as a grouped bar chart comparing sixes and fours per team side by side.

---

## 4. Batsmen Analysis (Player-Level)

### 4.1 Top 10 Run Scorers in IPL 2026

| Rank | Batsman | Total Runs |
|---|---|---|
| 1 | **Vaibhav Sooryavanshi** | 797 |
| 2 | Shubman Gill | 772 |
| 3 | Sai Sudharsan | 760 |
| 4 | Virat Kohli | 712 |
| 5 | Heinrich Klaasen | 647 |

> Visualised as a horizontal bar chart (`lightblue`).

### 4.2 Top Batsmen by Sixes Hit

| Rank | Batsman | Sixes |
|---|---|---|
| 1 | **Vaibhav Sooryavanshi** | 72 |
| 2 | Abhishek Sharma | 43 |
| 3 | Rajat Patidar | 42 |
| 4 | Ryan Rickelton | 38 |
| 5 | Mitchell Marsh | 36 |

> The same `is_six` column was reused by setting `b = 'is_six'` and applying the same groupby pattern, making the code reusable for any boundary type.

### 4.3 Strike Rate of Top Batsmen

**Formula:** `Strike Rate = (Runs Scored / Balls Faced) × 100`

**Filter:** Only batsmen with **≥ 30 balls faced** were included to ensure statistical significance.

| Rank | Batsman | Runs | Balls | Strike Rate |
|---|---|---|---|---|
| 1 | **Vaibhav Sooryavanshi** | 776 | 342 | **227** |
| 2 | Finn Allen | 349 | 168 | 208 |
| 3 | Priyansh Arya | 364 | 181 | 201 |
| 4 | Urvil Patel | 129 | 67 | 193 |
| 5 | Abhishek Sharma | 563 | 301 | 187 |

> Vaibhav Sooryavanshi dominated all three batting metrics — most runs, most sixes, and highest strike rate.

---

## 5. Bowler Analysis

### 5.1 Most Wickets Taken

> **Note:** Run-outs and "obstructing the field" dismissals were explicitly excluded since they are not credited to the bowler.

```python
bowler_wickets = df.loc[
    (df['wicket_type'].notnull()) &
    (df['wicket_type'] != 'runout') &
    (df['wicket_type'] != 'obstructing the field')
]
```

| Rank | Bowler | Wickets |
|---|---|---|
| 1 | **Kagiso Rabada** | 29 |
| 2 | Bhuvneshwar Kumar | 28 |
| 3 | Jofra Archer | 25 |
| 4 | Anshul Kamboj | 21 |
| 5 | Rashid Khan | 21 |

> Visualised as a red bar chart.

### 5.2 Best Economy Rate

**Formula:** `Economy Rate = (Runs Conceded / Balls Bowled) × 6`

**Filter:** Only bowlers with **≥ 18 legal balls** (3 overs) were included. Wides and no-balls were excluded from the ball count.

| Rank | Bowler | Runs | Balls | Economy Rate |
|---|---|---|---|---|
| 1 | **Saurabh Dubey** | 92 | 85 | **6.49** |
| 2 | Sunil Narine | 340 | 309 | 6.60 |
| 3 | Madhav Tiwari | 78 | 68 | 6.88 |
| 4 | Dilshan Madushanka | 32 | 27 | 7.11 |
| 5 | Anrich Nortje | 32 | 27 | 7.11 |

> Visualised as a 3-bar chart with `red`, `orange`, and `#FFD43B` (yellow) colours.

---

## 6. Wicket Type Breakdown

| Wicket Type | Count |
|---|---|
| **Caught** | 660 |
| Bowled | 137 |
| Run Out | 38 |
| LBW | 30 |
| Stumped | 9 |

> The full list of wicket types in the dataset:
> `caught`, `bowled`, `runout`, `lbw`, `stumped`, `retired hurt`, `obstructing the field`, `hitwicket`, `hit wicket`

> Visualised as a **pie chart** using `plt.pie()` with wicket-type labels.
> **Caught** dismissals dominate, accounting for the vast majority of wickets — a typical T20 pattern.

---

## 7. Over-by-Over Analysis

### Average Run Rate Per Over

An `over_number` column was derived from the `over` float column by casting `(over + 1).astype(int)`.

| Over | Avg Runs/Ball |
|---|---|
| 1 | 1.39 |
| 2 | 1.54 |
| 3 | 1.64 |
| 4 | 1.71 |
| 5 | 1.67 |
| ... | ... |

> Visualised as a **line plot** with markers (`marker='o'`), grid enabled, x-axis ticks set from 1–20.
> The pattern typically shows lower scoring in early overs, rising in the middle, and spiking in death overs.

---

## 8. Phase-wise Run Scoring by Team

### Total Runs by Phase (Pivot Table)

| Team | Powerplay (1–6) | Middle Overs (7–15) | Death Overs (16–20) |
|---|---|---|---|
| CSK | 839 | 1,069 | 615 |
| DC | 727 | 1,155 | 670 |
| **GT** | **976** | **1,411** | **696** |
| KKR | 724 | 1,040 | 547 |
| LSG | 862 | 1,002 | 641 |
| MI | 778 | 1,141 | 633 |
| PBKS | 853 | 1,162 | 689 |
| **RCB** | **1,000** | **1,359** | **695** |
| **RR** | **1,119** | **1,312** | **640** |
| SRH | 995 | 1,361 | 685 |

### Key Observations

- **GT** was dominant across all three phases, scoring the most runs in Powerplay and Middle overs.
- **RR** had the best Powerplay performance (1,119 runs), suggesting an aggressive opening approach.
- **KKR** scored the fewest runs in all three phases — indicating struggles throughout the tournament.
- **Middle overs** consistently accounted for the largest share of team totals across all sides.

> Two approaches were used to generate this table:
> 1. `groupby(['batting_team', 'phase_group'])` → long format
> 2. `pivot_table(index='batting_team', columns='phase_group', values='total_runs', aggfunc='sum')` → wide/pivot format
>
> Both were visualised as a **grouped bar chart** with three colour-coded bars per team (Powerplay in `#4682B4`, Middle overs and Death overs in other colours).

---

## 🛠 Technical Notes

- The notebook uses **cell-by-cell execution** (cells numbered In [1] through In [70]).
- Several cells were left blank (In [ ]) — placeholders or skipped analyses.
- The same groupby pattern was reused throughout (`df.groupby(...).agg(...).reset_index()`), making the code modular and readable.
- Visualisations were produced using both `plt.bar()` for single/grouped bars and `plt.plot()` for the over-by-over trend line.
- The strike rate analysis (`≥30 balls`) and economy rate analysis (`≥18 balls`) both apply minimum thresholds to avoid misleading statistics from small samples.
