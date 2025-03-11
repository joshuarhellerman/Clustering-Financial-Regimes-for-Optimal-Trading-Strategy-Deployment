# Regime-Adaptive Forex Strategy Pipeline 🚀

[![Python Version](https://img.shields.io/badge/python-3.7%2B-blue)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-lightgrey)](LICENSE)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

A sophisticated quantitative trading system that leverages machine learning to identify distinct market regimes in forex and automatically deploy optimized trading strategies for each regime. Built on a modular, extensible architecture supporting multiple currencies, timeframes, and trading strategies.

![Pipeline Overview](https://i.imgur.com/placeholder.png)

## 🔑 Key Features

- **Market Regime Detection**: Automatically identifies distinct market regimes using HDBSCAN clustering
- **Strategy-Regime Matching**: Optimizes strategy selection based on detected market conditions
- **End-to-End Pipeline**: From data acquisition to strategy deployment in one integrated system
- **Modular Architecture**: Easily extend with new strategies, features, or currency pairs
- **Impressive Results**: Achieves Sharpe ratios up to 4.57 in specific market regimes

## 📋 Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Pipeline Architecture](#pipeline-architecture)
- [Results](#results)
- [Scaling Potential](#scaling-potential)
- [Contributing](#contributing)
- [License](#license)

## 🔧 Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Basic Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/forex-regime-pipeline.git
cd forex-regime-pipeline

# Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate

# Install required packages
pip install -r requirements.txt
```

### Docker Installation (Alternative)

```bash
# Build the Docker image
docker build -t forex-regime-pipeline .

# Run the container
docker run -it forex-regime-pipeline
```

## 🚀 Usage

The pipeline consists of multiple sequential steps that can be run individually or as a complete workflow.

### Data Collection

```bash
# Fetch historical forex data
python data_collection.py --symbols EURUSD,GBPUSD,USDJPY,AUDUSD --years 1 --interval 5min
```

### Feature Engineering

```bash
# Generate features from raw price data
python feature_engineering.py --input "*_5min.csv" --output "*_features.csv"
```

### Feature Transformation

```bash
# Transform and normalize features
python feature_transformation.py --input "*_5min_features.csv" --nan_threshold 0.2
```

### Feature Selection

```bash
# Select stable, predictive features using walk-forward analysis
python feature_selection.py --input "*_transformed.csv"
```

### Regime Clustering

```bash
# Identify market regimes using HDBSCAN
python regime_clustering.py --input "*_selected.csv"
```

### Backtest Strategies

```bash
# Run backtests with regime-specific strategy optimization
python backtest.py --input "*_clustered_full.csv" --output "backtest_results"
```

### Complete Pipeline

```bash
# Run the entire pipeline from data collection to backtesting
python run_pipeline.py --symbols EURUSD,GBPUSD --years 1 --interval 5min
```

### Configuration

Create a `config.yaml` file to customize pipeline parameters:

```yaml
data:
  symbols: ["EURUSD", "GBPUSD", "USDJPY", "AUDUSD"]
  timeframe: "5min"
  years: 1

feature_engineering:
  categories: ["price", "volatility", "momentum", "trend", "cyclical", "statistical"]

clustering:
  algorithm: "hdbscan"
  min_cluster_size: 50
  min_samples: 12
  
strategies:
  enabled: ["TrendFollowing", "MeanReversion", "Breakout", "Momentum", "Scalping"]
  
backtesting:
  risk_free_rate: 0.01
  trading_costs: true
```

## 📊 Pipeline Architecture

Our systematic trading framework consists of five interconnected components:

### 1. Data Acquisition & Feature Engineering

**Methodology**:
- Multi-timeframe forex price data (5-minute granularity focus)
- Comprehensive feature generation (~50 features) across multiple categories:
  - Price action features (candlestick patterns, Heikin-Ashi)
  - Volatility metrics (ATR, Bollinger Band width)
  - Momentum indicators (RSI, MACD, Stochastics)
  - Trend measurements (ADX, moving averages)
  - Statistical features (z-scores, kurtosis, skewness)
  - Cyclical pattern detection (FFT-based features)

### 2. Feature Transformation & Selection

**Methodology**:
- Standardization and normalization of features
- Walk-forward feature selection using XGBoost importance scoring
- Stability-based feature filtering to avoid ephemeral patterns
- Regime-specific feature subset creation

### 3. Market Regime Clustering

**Methodology**:
- HDBSCAN (Hierarchical Density-Based Spatial Clustering of Applications with Noise)
- Adaptive hyperparameter tuning for regime detection
- Silhouette score validation for cluster quality
- Transition probability matrix calculation

### 4. Strategy-Regime Matching

**Methodology**:
- Library of adaptive strategy algorithms:
  - Trend Following (optimized for trending regimes)
  - Mean Reversion (optimized for range-bound regimes)
  - Breakout (optimized for volatility expansion regimes)
  - Momentum (optimized for directional strength regimes)
  - Scalping (optimized for low-volatility regimes)
- Regime characteristic analysis (volatility, directional bias, liquidity)
- Strategy-regime fitness evaluation

### 5. Deployment Optimization

**Methodology**:
- Dynamic strategy parameter adaptation to regime characteristics
- Regime transition detection and probabilistic forecasting
- Risk-adjusted position sizing based on regime volatility
- Trading cost model incorporating spread, commission, and slippage

## 📈 Results

Initial backtests on GBPUSD 5-minute data demonstrate the system's ability to generate alpha across different market regimes:

| Regime ID | Primary Strategy | Sharpe Ratio | Win Rate | Market Characteristics |
|-----------|------------------|--------------|----------|------------------------|
| 0 | TrendFollowing | 0.10 | 49.9% | Low volatility, neutral bias |
| 1 | Breakout | 0.24 | 27.2% | Morning European session |
| 2 | Breakout | 0.52 | 26.6% | Trending with moderate volatility |
| 3 | Breakout | 0.32 | 28.9% | Range expansion |
| 4 | Momentum | 1.49 | 11.1% | High volatility, strong directional moves |
| 5 | Scalping | 1.05 | 35.7% | Early US session |
| 6 | Scalping | 4.57 | 40.9% | Low noise, clear price action |
| 7 | Momentum | 2.59 | 40.4% | Strong trend with pullbacks |

The performance heatmap reveals a clear pattern of strategy-regime synergy:

![Strategy-Regime Performance Heatmap](https://i.imgur.com/placeholder2.png)

## 📦 Project Structure

```
forex-regime-pipeline/
├── data/                      # Raw and processed data
├── notebooks/                 # Jupyter notebooks for analysis
├── results/                   # Backtest results and visualizations
├── forex_regime_pipeline/     # Main package
│   ├── __init__.py
│   ├── data_collection.py     # Data acquisition module
│   ├── feature_engineering.py # Feature creation module
│   ├── feature_transformation.py # Feature normalization
│   ├── feature_selection.py   # Feature importance analysis
│   ├── regime_clustering.py   # Market regime detection
│   ├── strategies/            # Trading strategies
│   │   ├── __init__.py
│   │   ├── base.py            # Base strategy class
│   │   ├── trend_following.py # Trend following strategy
│   │   ├── mean_reversion.py  # Mean reversion strategy
│   │   ├── breakout.py        # Breakout strategy
│   │   ├── momentum.py        # Momentum strategy
│   │   └── scalping.py        # Scalping strategy
│   ├── backtesting/           # Backtesting engine
│   └── utils/                 # Utility functions
├── config.yaml                # Configuration file
├── run_pipeline.py            # End-to-end pipeline script
├── requirements.txt           # Package dependencies
├── setup.py                   # Package setup
└── README.md                  # This file
```

## 🔄 Scaling Potential

Our current implementation represents a foundation that can be scaled in multiple dimensions:

### 1. Cross-Pair Expansion

The existing architecture can be extended across all major, minor, and exotic forex pairs. Initial testing on EURUSD, GBPUSD, USDJPY, and AUDUSD demonstrates robust performance across different currency characteristics.

### 2. Multi-Timeframe Integration

A critical enhancement would be the integration of nested timeframe analysis:

- Higher timeframes (H1, H4, Daily) providing context and bias
- Medium timeframes (15min, 30min) for entry timing optimization
- Lower timeframes (1min, 5min) for execution optimization

### 3. Alternative Data Integration

The feature engineering component can be expanded to incorporate:

- Order flow data and market microstructure metrics
- Sentiment indicators from news flow analysis
- Macroeconomic data with varying release frequencies
- Volatility surface information from options markets

### 4. Machine Learning Enhancements

Several advanced ML techniques could further improve performance:

- Recurrent neural networks for sequential pattern recognition
- Reinforcement learning for dynamic strategy parameter optimization
- Explainable AI methods to extract trading rules from black-box models
- Ensemble methods combining multiple regime detection algorithms

## 🛠️ Development Roadmap

- [x] Core pipeline implementation
- [x] Basic strategy library
- [x] Regime detection optimization
- [ ] Cross-pair analysis toolkit
- [ ] Multi-timeframe integration
- [ ] Live trading interface
- [ ] Performance dashboard
- [ ] Advanced regime forecasting

## ✨ Contributing

Contributions are welcome for non-commercial use only. Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure your code follows the project's coding standards and includes appropriate tests.

## 📝 License

This project is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0) - see the [LICENSE](LICENSE) file for details.

### License Summary:

- **You are free to**:
  - Share — copy and redistribute the material in any medium or format
  - Adapt — remix, transform, and build upon the material

- **Under the following terms**:
  - Attribution — You must give appropriate credit, provide a link to the license, and indicate if changes were made
  - NonCommercial — You may not use the material for commercial purposes
  - ShareAlike — If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original

This is a human-readable summary of (and not a substitute for) the [full license](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode).

## 🙏 Acknowledgements

- [HDBSCAN](https://github.com/scikit-learn-contrib/hdbscan) for density-based clustering
- [XGBoost](https://github.com/dmlc/xgboost) for feature importance analysis
- [pandas-ta](https://github.com/twopirllc/pandas-ta) for technical analysis indicators
- [scikit-learn](https://github.com/scikit-learn/scikit-learn) for machine learning components
- [matplotlib](https://github.com/matplotlib/matplotlib) and [seaborn](https://github.com/mwaskom/seaborn) for visualizations

## 📞 Contact

Project Link: https://github.com/joshuarhellerman/Clustering-Financial-Regimes-for-Optimal-Trading-Strategy-Deployment.git

If you have any questions or feedback, please open an issue in the repository.
