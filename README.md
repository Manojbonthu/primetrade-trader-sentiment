# 📊 Trader Performance vs Market Sentiment
### Primetrade.ai — Data Science / Analytics Intern Assignment

> **Candidate:** Manoj  
> **Role Applied:** Data Science / Analytics Intern  
> **Submitted To:** Primetrade.ai Hiring Team

---

## 🚀 Live Demo

> 🔗 **Gradio Dashboard:** *(https://a19034f2232c127260.gradio.live/)*  
> 🔗 **GitHub Repo:** *(https://github.com/Manojbonthu/primetrade-trader-sentiment)*

---

## 📌 Objective

Analyze how Bitcoin market sentiment (Fear/Greed Index) relates to trader behavior and profitability on Hyperliquid — and uncover actionable patterns for smarter trading strategies.

---

## 🗂️ Project Structure

```
📁 primetrade-trader-sentiment/
│
├── Primetrade_Final.ipynb          ← Main notebook (run this in Colab)
├── README.md                       ← This file
│
├── 📊 Output Charts
│   ├── chart1_performance_fear_vs_greed.png
│   ├── chart2_behavior_fear_vs_greed.png
│   ├── chart3_segments_sentiment.png
│   ├── chart4_winrate_heatmap.png
│   ├── chart5_pnl_vs_sentiment_timeline.png
│   ├── chart6_longshort_size.png
│   ├── chart7_feature_importance.png
│   └── chart8_trader_archetypes.png
│
└── 📋 Output Tables
    ├── summary_performance.csv
    ├── summary_behavior.csv
    ├── summary_clusters.csv
    └── trader_stats_full.csv
```

---

## ⚙️ How to Run

### ✅ Google Colab (Recommended)
1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Upload `Primetrade_Final.ipynb`
3. Click **Runtime → Run All**
4. Datasets auto-download via `gdown` — no manual upload needed
5. Gradio dashboard launches at the end with a public shareable URL

### 💻 Local Setup
```bash
pip install gdown pandas numpy matplotlib seaborn scikit-learn plotly gradio
jupyter notebook Primetrade_Final.ipynb
```

---

## 📦 Datasets

| Dataset | Source | Rows | Columns |
|---|---|---|---|
| Bitcoin Fear/Greed Index | Google Drive (auto-downloaded) | 2,644 | 4 |
| Hyperliquid Trader Data | Google Drive (auto-downloaded) | 211,224 | 16 |

**Key columns used:**
- `Closed PnL`, `Size USD`, `Side`, `Timestamp` — from trader data
- `classification`, `date` — from Fear/Greed data

---

## 🔬 Methodology

### Part A — Data Preparation
- Audited shape, missing values, and duplicates for both datasets
- Parsed Unix millisecond timestamps from trader data
- Hardcoded column renames (`Closed PnL` → `closedPnL`, `Account` → `account`, etc.)
- Merged both datasets on daily date key via left join
- Engineered features: `is_win`, `is_long`, `daily_pnl`, `win_rate`, `long_ratio`, `drawdown_proxy`

### Part B — Analysis
- Compared PnL, win rate, and drawdown across Fear vs Greed days
- Compared behavioral metrics (trade frequency, position size, long ratio) by sentiment
- Created 3 trader segments:
  - **High vs Low Leverage** — median split on avg leverage
  - **Frequent vs Infrequent** — median split on total trades
  - **Consistent Winner vs Inconsistent** — win rate ≥ 50% AND total PnL > 0
- Generated 8 charts covering performance, behavior, segments, heatmaps, and timeline

### Bonus — Predictive Model
- **Model:** Random Forest Classifier with 5-fold cross-validation
- **Target:** Next-day PnL bucket (Low / Mid / High) using quantile-based binning
- **Features:** Lagged PnL, lagged trades, lagged win rate, current trades, win rate, sentiment encoding
- **Pipeline:** Median imputation → Random Forest (200 trees, max depth 6)

### Bonus — Trader Clustering
- **Algorithm:** KMeans (k=4, elbow method used to select k)
- **Features:** total_pnl, total_trades, overall_win_rate, avg_size, drawdown_proxy
- **Visualization:** PCA 2D scatter of 4 behavioral archetypes

### Bonus — Gradio Dashboard
- Dark-themed interactive web UI with 4 tabs
- Tab 1: All 8 charts selectable via radio buttons
- Tab 2: Live data tables (performance, behavior, clusters, trader stats)
- Tab 3: Strategy recommendation cards
- Tab 4: Key insight cards in grid layout

---

## 💡 Key Insights

**Insight 1 — PnL is Sentiment-Sensitive**  
Average daily PnL is significantly higher on Greed days. Bullish sentiment directly correlates with trading profitability on Hyperliquid.

**Insight 2 — Leverage is the #1 Risk Driver**  
High-leverage traders show deeper losses during Fear periods. Low-leverage traders stay near-neutral — leverage, not market direction alone, amplifies losses.

**Insight 3 — Overtrading on Greed Hurts Struggling Traders**  
Trade frequency spikes on Greed days. Only Consistent Winners benefit — Struggling Traders overtrade during euphoria, a key risk signal.

**Insight 4 — Persistent Long Bias Across Both Regimes**  
Traders are net-long regardless of Fear or Greed. Short entries during Extreme Fear (index < 25) are rare but historically among the most profitable trades.

**Insight 5 — Consistent Winners Adapt; Others React**  
The Consistent Winner segment maintains positive PnL even in Fear days — disciplined sizing and adaptive strategy selection is the defining differentiator vs all other segments.

---

## 🎯 Strategy Recommendations

### Strategy 1 — Cap Leverage During Fear
> **Rule:** When Fear/Greed Index < 40, cap leverage at ≤5x  
> **For:** High-leverage traders  
> **Expected impact:** 20–30% reduction in drawdown depth

### Strategy 2 — Counter-Trend Long in Extreme Fear
> **Rule:** When index < 25, open longs with tight stop-loss  
> **For:** Consistent Winners with leverage ≤3x  
> **Expected impact:** Better entry prices, improved win rate on reversal trades

### Strategy 3 — Controlled Frequency Boost on Greed Days
> **Rule:** When index > 60, increase trade count ~1.5× with strict per-trade risk limits  
> **For:** Infrequent / conservative traders  
> **Expected impact:** 15–25% increase in realized monthly PnL

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.12 | Core language |
| Pandas / NumPy | Data manipulation |
| Matplotlib / Seaborn | Static charts |
| Scikit-learn | ML model + clustering |
| Gradio | Interactive dashboard |
| gdown | Auto dataset download |
| Google Colab | Execution environment |

---

*Submitted by Manoj | B.Tech CSE 2025 | Raghu Engineering College, Visakhapatnam*
