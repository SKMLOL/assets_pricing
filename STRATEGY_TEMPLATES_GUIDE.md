# Strategy Templates Guide

This repository now contains **6 different trading strategy templates** for backtesting and optimization. Each template follows the same structure but implements a different trading strategy.

## Available Templates

### 1. template_3EMA.ipynb (Original - Updated)
**Strategy:** Triple EMA Crossover  
**Logic:** Buy when any EMA crosses above another, sell when any crosses below  
**Parameters:**
- EMA1 (Fast): 4-39 periods (step 5)
- EMA2 (Medium): 50-85 periods (step 5)  
- EMA3 (Slow): 120-245 periods (step 5)
- **Total combinations:** 1,664

**Use case:** Trend-following with multiple timeframe confirmation

---

### 2. template_MACD.ipynb (New)
**Strategy:** MACD Crossover  
**Logic:** Buy when MACD line crosses above signal line, sell when crosses below  
**Parameters:**
- Fast EMA: 8-18 periods (step 2)
- Slow EMA: 20-32 periods (step 3)
- Signal Line: 7-12 periods (step 1)
- **Total combinations:** ~400

**Use case:** Momentum-based trading with convergence/divergence signals

---

### 3. template_MA_price_ratio.ipynb (New)
**Strategy:** MA/Price Ratio  
**Logic:** Buy when Price/MA ratio crosses above threshold, sell when crosses below  
**Parameters:**
- MA Period: 20-200 periods (step 10)
- Threshold: 0.95-1.04 (step 0.01)
- **Total combinations:** ~190

**Use case:** Mean-reversion trading based on price deviation from moving average

---

### 4. template_TSMOM.ipynb (New)
**Strategy:** Time Series Momentum (TSMOM)  
**Logic:** Buy when recent return is positive, sell when negative  
**Parameters:**
- Lookback Period: 10-120 periods (step 10)
- Holding Period: 5-40 periods (step 5)
- **Total combinations:** ~96

**Use case:** Pure momentum strategy based on recent price trends

---

### 5. template_simple_MA.ipynb (New)
**Strategy:** Simple MA Crossover  
**Logic:** Buy when price crosses above MA, sell when crosses below  
**Parameters:**
- MA Period: 10-205 periods (step 5)
- **Total combinations:** 40

**Use case:** Classic trend-following with single moving average

---

### 6. template_double_MA.ipynb (New)
**Strategy:** Double MA Crossover  
**Logic:** Buy when fast MA crosses above slow MA, sell when crosses below  
**Parameters:**
- Fast MA: 5-50 periods (step 5)
- Slow MA: 20-210 periods (step 10)
- **Total combinations:** ~200

**Use case:** Traditional dual moving average crossover system

---

## How to Use

### 1. Setup Your Data
Each template expects a CSV file with your asset data:

```python
# Modify these parameters in Cell 3:
START_DATE = '2017-01-01'    # Start date for analysis
END_DATE = '2024-06-21'      # End date for analysis
DATA_PATH = r"data/QQQ.csv"  # Path to your CSV file
```

**Required CSV format:**
- Index: Date (datetime)
- Columns: Must include either `Close` or `close` (case-insensitive handling)
- Optional: `Open`, `High`, `Low`, `Volume` (also case-insensitive)

### 2. Adjust Train/Validation Split
```python
# Cell 4:
TRAIN_RATIO = 0.60  # 60% for training, 40% for validation
```

### 3. Run the Grid Search
Each template will:
1. Load and prepare your data
2. Generate all parameter combinations
3. Run backtests on training data (with progress bar)
4. Display top 10 strategies ranked by Sharpe ratio
5. Validate best strategy on validation set
6. Show full sample backtest results
7. Provide trade-by-trade analysis

### 4. Review Results
The templates provide:
- **Top 10 strategies** by Sharpe ratio
- **Best strategy** parameters and metrics
- **Validation performance** (out-of-sample)
- **Full sample backtest** with equity curve
- **Trade analysis** with win rate, avg win/loss, etc.

---

## Key Features (All Templates)

✅ **No Yahoo Finance dependency** - Use your own CSV data  
✅ **Robust column handling** - Works with Close/close, Volume/volume  
✅ **Lookahead bias protection** - Signals shifted by 1 bar  
✅ **Progress bars** - Real-time grid search status with tqdm  
✅ **Train/validation split** - Prevents overfitting  
✅ **Comprehensive metrics** - Sharpe, Sortino, Calmar, win rate, etc.  
✅ **Transaction costs** - Includes fees (0.05%) and slippage (0.05%)  
✅ **Synoptical output** - Concise, easy-to-read results  

---

## Common Cell Structure

All templates follow this structure:

- **Cell 1-2:** Imports and dependencies
- **Cell 3:** Data loading from CSV
- **Cell 4:** Price series preparation and train/val split
- **Cell 5:** Strategy parameter definition
- **Cell 6:** Results collection system setup
- **Cell 7:** Visualization parameters
- **Cell 8:** Grid search execution (with tqdm)
- **Cell 9:** Top results display
- **Cell 10:** Validation on test set
- **Cell 11:** Train vs validation comparison
- **Cell 12:** Full sample backtest
- **Cell 13:** Trade-by-trade analysis
- **Cell 14+:** Additional visualizations and sensitivity analysis

---

## Tips for Best Results

1. **Start with default parameters** to understand each strategy
2. **Adjust parameter ranges** based on your asset's characteristics
3. **Use sufficient training data** (recommended: 3+ years)
4. **Monitor validation performance** - high train but low validation = overfitting
5. **Consider transaction costs** - already included at 0.05% + 0.05%
6. **Test on multiple assets** to find robust strategies
7. **Combine strategies** for portfolio diversification

---

## Example Workflow

```python
# 1. Prepare your data
# Save asset data as CSV with Date index and Close column

# 2. Open desired template
# jupyter notebook template_MACD.ipynb

# 3. Update data path (Cell 3)
DATA_PATH = r"data/AAPL.csv"

# 4. Run all cells
# The grid search will show progress and find optimal parameters

# 5. Review results
# Check if validation Sharpe > 0.5 (good)
# Check if train and validation performance are similar (not overfit)

# 6. Apply to other assets
# Repeat with different CSV files
```

---

## Customization

You can easily modify:
- Parameter ranges (Cell 5/6)
- Train/validation ratio (Cell 4)
- Transaction costs in grid search cells
- Optimization target (change from Sharpe to Sortino, etc.)
- Date ranges for analysis

---

## Performance Metrics Explained

- **Sharpe Ratio:** Risk-adjusted return (higher is better, >1 is good)
- **Sortino Ratio:** Like Sharpe but only penalizes downside volatility
- **Calmar Ratio:** Return / Max Drawdown
- **Max Drawdown:** Largest peak-to-trough decline (lower is better)
- **Win Rate:** Percentage of winning trades
- **Profit Factor:** Gross profit / Gross loss (>1 means profitable)
- **Expectancy:** Average expected return per trade

---

## Download and Test

Each template is a standalone Jupyter notebook that you can:
1. Download directly from the repository
2. Open in Jupyter/JupyterLab
3. Modify for your specific needs
4. Run independently

No dependencies between templates - choose the strategies you want to test!

---

*Last updated: December 2024*
