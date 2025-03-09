# Market Regime Analysis Toolkit

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache%202.0-green)](https://opensource.org/licenses/Apache-2.0)

A professional-grade pipeline for identifying, validating, and analyzing financial market regimes using machine learning and statistical methods.

![Market Regime Analysis Concept](https://via.placeholder.com/1200x600.png?text=Market+Regime+Analysis+Visualization) *Example visualization placeholder*

## Key Features ✨

- **Automated Regime Detection**  
  Cluster market conditions using volatility, trend strength, and liquidity features with configurable thresholds

- **Statistical Validation**  
  Hypothesis testing with Mann-Whitney U tests and Benjamini-Hochberg multiple testing correction

- **Interpretable Insights**  
  Natural language regime descriptions with risk assessments and temporal patterns

- **Professional Visualizations**  
  Interactive Plotly charts for regime characteristics, feature significance, and component distributions

- **Production-Ready Architecture**  
  Robust error handling, data validation, and modular OOP design

## Tech Stack 🛠️

- **Core**: Python 3.8+, Pandas, NumPy
- **Machine Learning**: UMAP (cluster visualization), automated feature engineering
- **Statistics**: SciPy, Statsmodels (multiple testing correction)
- **Visualization**: Plotly (interactive HTML reports)
- **Infrastructure**: Configurable parameters, type hints, comprehensive logging

## Installation 📦

```bash
# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate  # Linux/MacOS
.\.venv\Scripts\activate   # Windows

# Install dependencies
pip install umap-learn plotly pandas numpy scipy statsmodels tqdm

Usage 🚀
Basic Analysis Pipeline

from analyzer import MarketRegimeAnalyzer

# Initialize analyzer with results directory
analyzer = MarketRegimeAnalyzer(results_dir="validation_results")

# Load and validate data
analyzer.load_data()

# Generate interactive visualizations
analyzer.plot_regime_characteristics().show()
analyzer.plot_significance_heatmap().show()

Key Functionality

# Get statistical summary of market regimes
component_analysis = analyzer.get_component_analysis()
print(component_analysis.head())

# Generate sample size distribution plot
analyzer.plot_sample_sizes().show()

# Export regime characteristics to CSV
analyzer.report_data.to_csv("regime_analysis.csv", index=False)

Visualizations 📊
Regime Characteristics
Comparative box plots showing distributions of:

Average returns

Volatility ranks

Maximum drawdowns

Regime durations

Feature Significance Heatmap
Interactive matrix showing statistically significant features across currency pairs

Component Distribution Treemap
Hierarchical visualization of market regime components (volatility, trend direction, risk levels)

Sample Size Distribution
Bar chart showing observation counts per identified regime

Contributing 🤝
We welcome contributions following these guidelines:

Code Quality

PEP8 compliance (black formatting recommended)

Comprehensive type hints

Google-style docstrings

Testing

Unit tests for new features (pytest)

Type checking with mypy

Benchmarking for performance-critical code

Workflow

Open an issue to discuss proposed changes

Branch from develop using feature/ prefix

Submit PR with updated documentation and tests

License 📄
Apache 2.0 - See LICENSE for full details

Disclaimer ⚠️
This project is intended for educational and research purposes only. It does not constitute financial advice, and users are solely responsible for any investment decisions made using this software. Always consult with a qualified financial advisor before making trading decisions.
