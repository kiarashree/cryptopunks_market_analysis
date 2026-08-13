# Punks Market Analysis

### From web scraping to market modelling - what actually drives CryptoPunks prices?

Built this project to investigate how **rarity, liquidity, Ethereum exposure, and market regimes** influence CryptoPunks prices and trading behaviour.

Instead of downloading a ready-made dataset, I built the data pipeline myself - scraping CryptoPunks transaction histories, storing them in **SQLite**, engineering rarity and market features, and then applying statistical and trading analysis.

**303 CryptoPunks · 11,587 transactions · End-to-end Python pipeline**

## Project Pipeline

```text
CryptoPunks Web Pages
        ↓
Selenium + BeautifulSoup
        ↓
Transaction & Attribute Extraction
        ↓
SQLite Database
        ↓
Cleaning & Feature Engineering
        ↓
Rarity + Liquidity Analysis
        ↓
ETH & Market Data Integration
        ↓
Hedonic Pricing Model
        ↓
Repeat-Sales & Trading Analysis
```

---

## Building the Dataset

A custom **headless Selenium scraper** was built to collect transaction histories directly from individual CryptoPunks pages.

The pipeline:

- Navigates dynamically generated pages using **Selenium**
- Parses HTML with **BeautifulSoup**
- Identifies sales, bids, offers, transfers, and withdrawn bids
- Extracts transaction dates
- Parses both **ETH and USD values**
- Associates every transaction with its Punk ID
- Stores structured records directly in **SQLite**

So yes, before analysing the data, I had to actually go and get it.

## Feature Engineering

CryptoPunk attributes were transformed into several measures of rarity:

- **Rarest Active Trait**
- **Attribute Count**
- **Inverse-Frequency Rarity**
- **Log-Sum Rarity**

These features were used to test whether scarcity actually translates into higher market valuations.

## Key Results

| Metric | Result |
|---|---:|
| CryptoPunks analysed | **303** |
| Transactions analysed | **11,587** |
| Pricing-model observations | **640** |
| R² | **0.895** |
| Adjusted R² | **0.894** |
| ETH coefficient | **1.58** |
| Estimated rarity premium | **~44%** |
| Repeat-sale pairs | **661** |

The hedonic model explained approximately **89.5% of variation in log NFT prices** using structural rarity, NFT market conditions, and Ethereum price.

## ETH Mattered. A Lot.

The estimated ETH coefficient was approximately **1.58**.

Within the model, a **1% increase in ETH price was associated with roughly a 1.58% increase in CryptoPunk price**, holding the other model variables constant.

Rarity mattered too — but the bigger story was:

> **Rarity helped explain which Punks were expensive. Market conditions helped explain when they became expensive.**

## Pricing Analysis

### Rarity vs Price

![Rarity vs Price](results/rarity_vs_price.png)

Rarity has a positive relationship with price, but the dispersion makes something clear: **rare doesn't automatically mean expensive.**

### Actual vs Fitted Prices

![Actual vs Fitted Prices](results/actual_vs_fitted.png)

The model performs reasonably well around typical transactions but struggles with extreme prices — where liquidity and speculative behaviour become much more important.

## Liquidity Regimes

### Monthly Trading Activity

![Monthly CryptoPunks Sales](results/monthly_sales.png)

Trading activity accelerated dramatically during the **2021 NFT boom** before contracting, revealing a clear liquidity cycle.

### Cumulative Trading Returns

![Cumulative Trading Returns](results/cumulative_trading_returns.png)

Returns were concentrated around particular liquidity-expansion periods rather than appearing consistently through time.

## Repeat-Sales Analysis

I also implemented a repeat-sales approach to separate market-wide appreciation from differences between individual CryptoPunks.

The analysis produced:

**177 eligible CryptoPunks · 661 repeat-sale pairs**

The resulting index captured the rapid 2021 expansion, subsequent correction, and continued market volatility.

## Tech Stack

**Languages & Data**

`Python` `SQL` `Pandas` `NumPy`

**Data Engineering**

`Selenium` `BeautifulSoup` `SQLite` `Web Scraping`

**Modelling & Analytics**

`Statsmodels` `Regression` `Feature Engineering` `Time-Series Analysis` `Trading Analytics`

**Visualisation**

`Matplotlib`


## Repository Structure

```text
cryptopunks-market-analysis/
│
├── notebooks/
│   └── cryptopunks_market_analysis.ipynb
│
├── results/
│   ├── monthly_sales.png
│   ├── rarity_vs_price.png
│   ├── actual_vs_fitted.png
│   └── cumulative_trading_returns.png
│
├── data/
├── requirements.txt
└── README.md
```

---

## What I Took Away

CryptoPunks pricing wasn't simply **"rarer = more expensive."**

The evidence points toward an interaction between:

**Structural Scarcity × Crypto Exposure × Liquidity Regime**

And technically, the project gave me an opportunity to work across the entire pipeline:

**Web Scraping → SQL/SQLite → Data Cleaning → Feature Engineering → Statistical Modelling → Time-Series & Trading Analysis**

---

*Turns out even pixelated punks need proper risk analysis.*
