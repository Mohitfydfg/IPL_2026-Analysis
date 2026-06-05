# 🏏 IPL 2026 Data Analysis

A ball-by-ball exploratory data analysis of the **Indian Premier League 2026** season using Python. The project uncovers team and player performance trends across batting, bowling, boundaries, strike rates, economy rates, wicket patterns, and phase-wise scoring.

---

## 📸 Preview

> Analysis covers 74 matches · 17,477 deliveries · 10 teams · Full tournament (Group Stage → Final)

---

## 📁 Repository Structure

```
ipl-2026-analysis/
│
├── IPL_2026_Analysis.ipynb     # Main Jupyter Notebook
├── ipl_2026_deliveries.csv     # Ball-by-ball dataset
├── IPL_2026_Analysis_Summary.md # Detailed analysis summary
└── README.md
```

---

## 📊 Dataset

| Property | Value |
|---|---|
| File | `ipl_2026_deliveries.csv` |
| Rows | 17,477 deliveries |
| Columns | 21 |
| Season | IPL 2026 |
| Matches | 74 (Group Stage + Playoffs + Final) |
| Teams | 10 |
| Tournament Dates | Mar 28, 2026 – May 31, 2026 |
| Final Venue | Narendra Modi Stadium, Ahmedabad |
| Final | RCB vs GT |

### Columns

```
match_id, season, phase, match_no, date, venue,
batting_team, bowling_team, innings, over, striker, bowler,
runs_of_bat, extras, wide, legbyes, byes, noballs,
wicket_type, player_dismissed, fielder
```

---

## 🔧 Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical-013243?logo=numpy)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualisation-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4c72b0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)

---

## 🔍 Analysis Sections

### 1. 🧹 Feature Engineering
New columns derived from raw data:
- `total_runs` — runs per delivery (`runs_of_bat + extras`)
- `is_six` — binary flag for sixes
- `is_four` — binary flag for fours
- `is_wicket` — binary flag for wicket deliveries
- `phase_group` — over categorised as `Powerplay(1-6)`, `Middle_overs(7-15)`, or `Death_overs(16-20)`

---

### 2. 🏟️ Team Batting Analysis

**Most Runs by Team:**

| Rank | Team | Total Runs |
|---|---|---|
| 🥇 | GT | 3,083 |
| 🥈 | RR | 3,071 |
| 🥉 | RCB | 3,054 |
| 4 | SRH | 3,041 |

**Most Boundaries by Team:**

| Team | Sixes | Fours | Total |
|---|---|---|---|
| GT | 124 | 292 | **416** |
| CSK | 124 | 220 | 344 |
| DC | 117 | 225 | 342 |
| LSG | 127 | 208 | 335 |

---

### 3. 🏏 Batsmen Analysis

**Top Run Scorers:**

| Rank | Batsman | Runs |
|---|---|---|
| 🥇 | Vaibhav Sooryavanshi | 797 |
| 🥈 | Shubman Gill | 772 |
| 🥉 | Sai Sudharsan | 760 |
| 4 | Virat Kohli | 712 |
| 5 | Heinrich Klaasen | 647 |

**Top Six Hitters:**

| Rank | Batsman | Sixes |
|---|---|---|
| 🥇 | Vaibhav Sooryavanshi | 72 |
| 🥈 | Abhishek Sharma | 43 |
| 🥉 | Rajat Patidar | 42 |

**Highest Strike Rates** *(min. 30 balls faced)*:

| Rank | Batsman | SR |
|---|---|---|
| 🥇 | Vaibhav Sooryavanshi | 227 |
| 🥈 | Finn Allen | 208 |
| 🥉 | Priyansh Arya | 201 |

> Formula: `Strike Rate = (Runs / Balls) × 100`

---

### 4. 🎳 Bowler Analysis

**Most Wickets** *(run-outs excluded)*:

| Rank | Bowler | Wickets |
|---|---|---|
| 🥇 | Kagiso Rabada | 29 |
| 🥈 | Bhuvneshwar Kumar | 28 |
| 🥉 | Jofra Archer | 25 |
| 4 | Anshul Kamboj | 21 |
| 5 | Rashid Khan | 21 |

**Best Economy Rates** *(min. 18 legal balls)*:

| Rank | Bowler | Economy |
|---|---|---|
| 🥇 | Saurabh Dubey | 6.49 |
| 🥈 | Sunil Narine | 6.60 |
| 🥉 | Madhav Tiwari | 6.88 |

> Formula: `Economy Rate = (Runs / Balls) × 6`

---

### 5. 🎯 Wicket Type Breakdown

| Wicket Type | Count |
|---|---|
| Caught | 660 |
| Bowled | 137 |
| Run Out | 38 |
| LBW | 30 |
| Stumped | 9 |

> Visualised as a pie chart. Caught dismissals dominate — a typical T20 pattern.

---

### 6. 📈 Over-by-Over Run Rate

Average runs per ball across all 20 overs, visualised as a line chart. Early overs (1–2) show the lowest scoring; death overs see the biggest spikes.

---

### 7. 🔀 Phase-wise Scoring by Team

| Team | Powerplay | Middle | Death |
|---|---|---|---|
| CSK | 839 | 1,069 | 615 |
| DC | 727 | 1,155 | 670 |
| **GT** | **976** | **1,411** | **696** |
| KKR | 724 | 1,040 | 547 |
| LSG | 862 | 1,002 | 641 |
| MI | 778 | 1,141 | 633 |
| PBKS | 853 | 1,162 | 689 |
| RCB | 1,000 | 1,359 | 695 |
| **RR** | **1,119** | 1,312 | 640 |
| SRH | 995 | 1,361 | 685 |

**Key Takeaways:**
- GT dominated in Middle overs (1,411 runs)
- RR was the most aggressive in the Powerplay (1,119 runs)
- KKR struggled across all three phases

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Run the Notebook

```bash
git clone https://github.com/your-username/ipl-2026-analysis.git
cd ipl-2026-analysis
jupyter notebook IPL_2026_Analysis.ipynb
```

---

## 💡 Key Insights

- **Vaibhav Sooryavanshi** was the player of the tournament by every batting metric — most runs (797), most sixes (72), and highest strike rate (227).
- **GT** was the most dominant team overall, topping both total runs and boundary count.
- **Kagiso Rabada** was the most dangerous bowler with 29 wickets.
- **Saurabh Dubey** was the most economical, conceding just 6.49 runs per over.
- **Caught** dismissals accounted for the overwhelming majority of wickets (660 out of ~874), consistent with T20 cricket.
- **RR's aggressive Powerplay** approach (1,119 runs) stood out compared to teams like DC (727) and KKR (724).

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙌 Acknowledgements

- Data sourced from IPL 2026 ball-by-ball records
- Analysis inspired by the cricinfo/ESPNcricinfo style stat breakdowns

---

*Made with ❤️ and Python*
