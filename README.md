# us-etf-fund-analytics
ETF Analytics Pipeline

End-to-end analytics pipeline for evaluating 2,300+ ETFs and mutual funds using risk-adjusted, liquidity-aware scoring and percentile-based ranking.

Overview

This project builds a data pipeline that transforms raw ETF and mutual fund price data into structured, analysis-ready datasets.

Instead of using only returns, the system evaluates funds using a combination of:

Risk (volatility)
Return (average performance)
Liquidity (volume)

All metrics are standardized using percentile ranking to enable fair comparison across funds.

Key Features:
ETL pipeline for financial time-series data
Daily return and volatility computation
Percentile-based normalization for cross-fund comparison
Weighted scoring model for fund ranking
Quartile-based segmentation
Hidden gem detection logic
Category-level performance analysis
Export-ready datasets for BI tools (Tableau)

Tech Stack:
Python
Pandas
NumPy
Google Colab
CSV-based data pipeline
Tableau (downstream visualization)

Pipeline Workflow:
Load ETF and mutual fund datasets
Clean and preprocess time-series data
Calculate daily returns and rolling volatility
Aggregate fund-level performance metrics
Merge metadata (category, region, fund details)
Normalize metrics using percentile ranking
Compute weighted overall score
Rank and segment funds
Identify hidden gems
Export final datasets

Feature Engineering:
Returns
daily_return = (close - prev_close) / prev_close
Volatility

30-day rolling standard deviation of returns

Scoring System

Funds are ranked using a weighted percentile model:

overall_score = (
    0.6 * return_percentile +
    0.4 * risk_percentile
)

Return percentile: higher is better
Risk percentile: lower volatility is better (inverted ranking)

Hidden Gem Logic
A fund is classified as a Hidden Gem if:

Above median returns
Below median volatility
Below median trading volume

These represent high-quality but under-the-radar funds.

Outputs

Fund-Level Dataset
Includes:
Returns
Volatility
Liquidity
Percentile scores
Overall ranking
Segment classification
Hidden gem flag

Category Summary
Includes:
Category-wise performance metrics
Risk and return averages
Hidden gem counts
Category ranking
Output Files
gold_etf_table.csv
category_summary.csv
Key Insight

Percentile normalization allows heterogeneous financial instruments to be compared on a single standardized scale, improving interpretability and decision-making.

Future Improvements
Sharpe / Sortino ratio integration
Real-time market data ingestion
Factor-based risk modeling
ML-based fund clustering
Automated dashboard pipeline (Tableau / Power BI APIs)
