# 📈 FractalQuant — Market Regime Detection & Price Movement Prediction

**A quantitative finance dashboard combining fractal analysis, volatility modeling, and machine learning to study financial market behavior.**

FractalQuant leverages **Rescaled Range (R/S) Analysis** to estimate the Hurst Exponent of financial time series, identify market regimes, and extract temporal dependencies from historical price data. A Random Forest classifier then uses fractal-memory and volatility-based features to predict short-term price direction.

The goal is to connect the statistical properties of financial markets with interpretable machine learning in a unified analytical dashboard.

---

## 🚀 Key Features

- **Hurst Exponent Estimation** — Applies Rescaled Range (R/S) Analysis to measure long-term dependence in financial time series.
- **Market Regime Detection** — Classifies market behavior into trending, mean-reverting, or approximately random regimes based on the estimated Hurst Exponent.
- **Random Forest Classification** — Uses engineered features derived from fractal memory and volatility to estimate short-term upward or downward price movements.
- **Volatility Analysis** — Examines changes in return dispersion to characterize market conditions.
- **Interactive Dashboard** — Brings market statistics, regime signals, and model predictions together in one interface.
- **Quantitative Visualization** — Displays price trends, volatility patterns, and regime classifications to support exploratory analysis.

## 🧠 Methodology

### 1. Financial Time-Series Analysis

Historical price data is transformed into returns for statistical analysis.

For a price series \(P_t\), the log return is calculated as:

\[
r_t = \ln\left(\frac{P_t}{P_{t-1}}\right)
\]

Returns provide a consistent basis for studying dependence and volatility.

### 2. Hurst Exponent Using R/S Analysis

The Hurst Exponent \(H\) measures the scaling behavior of a time series and provides insight into its persistence.

The Rescaled Range statistic is defined as:

\[
(R/S)_n = \frac{\max(Y_k)-\min(Y_k)}{S_n}
\]

where \(Y_k\) is the cumulative sum of deviations from the sample mean and \(S_n\) is the sample standard deviation.

The scaling relationship is approximated by:

\[
\mathbb{E}[R/S]_n \propto n^H
\]

The exponent \(H\) is estimated from the slope of the log-log relationship between window size and the rescaled range.

### 3. Market Regime Classification

The estimated Hurst Exponent is used to characterize the statistical behavior of the market.

| Hurst Exponent | Interpretation |
|---|---|
| \(H > 0.5\) | Persistent behavior; trends may continue |
| \(H \approx 0.5\) | Random-walk-like behavior |
| \(H < 0.5\) | Anti-persistent behavior; reversals may be more likely |

These are statistical interpretations rather than guaranteed trading signals. Real-world regime classification depends on window size, data quality, and estimation uncertainty.

### 4. Feature Engineering

Fractal and volatility information is converted into features for machine learning. Depending on the implementation, these may include:

- Rolling Hurst Exponent estimates
- Historical return and momentum features
- Rolling volatility measures
- Lagged returns
- Market-regime indicators

Features should be computed using only information available at the prediction timestamp to prevent look-ahead bias.

### 5. Random Forest Prediction

A Random Forest classifier learns relationships between the engineered features and a defined future price-direction target.

For a chosen forecast horizon \(h\), a possible target is:

\[
y_t =
\begin{cases}
1, & P_{t+h} > P_t \\
0, & P_{t+h} \leq P_t
\end{cases}
\]

The model estimates the likelihood of an upward or downward movement based on historical patterns.

Prediction quality should be evaluated using chronological train/test splits and appropriate classification metrics, rather than random shuffling of time-series observations.

---

## 🏗️ System Architecture

```text
Historical Market Data
         │
         ▼
 Data Preprocessing
         │
         ▼
 Return & Volatility Analysis
         │
         ▼
 Hurst Exponent Estimation
         │
         ▼
 Market Regime Identification
         │
         ▼
 Feature Engineering
         │
         ▼
 Random Forest Classifier
         │
         ▼
 Price Direction Probabilities
         │
         ▼
 Interactive Quantitative Dashboard
```

## 📊 Model Evaluation

Model performance can be assessed using:

| Metric | Purpose |
|---|---|
| Accuracy | Overall proportion of correct predictions |
| Precision | Reliability of positive predictions |
| Recall | Ability to identify positive cases |
| F1-score | Balance between precision and recall |
| ROC-AUC | Ability to distinguish between classes |
| Confusion Matrix | Breakdown of correct and incorrect classifications |

For a more realistic financial assessment, consider transaction costs, slippage, turnover, maximum drawdown, and risk-adjusted returns if the model is evaluated as a trading strategy.

*Evaluation metrics should be reported from actual test results; no performance figures are assumed here.*

## 🛠️ Technology Stack

- **Language:** Python
- **Data Processing:** NumPy, Pandas
- **Machine Learning:** Scikit-learn
- **Visualization:** Matplotlib / Plotly
- **Dashboard:** Streamlit *(if used in the implementation)*
- **Financial Data:** Historical market-price data from the configured data source

## ⚙️ Getting Started

### Prerequisites

- Python 3.10 or a compatible version
- Git
- pip

### Installation

Clone the repository:

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

Install the project dependencies:

```bash
pip install -r requirements.txt
```

### Run the Dashboard

If the application uses Streamlit and the entry point is `app.py`:

```bash
streamlit run app.py
```

Adjust the command to match the actual dashboard entry point in your repository.

## 📁 Suggested Project Structure

```text
FractalQuant/
├── app.py
├── data/
├── src/
│   ├── data_loader.py
│   ├── hurst_analysis.py
│   ├── regime_detection.py
│   ├── feature_engineering.py
│   └── model.py
├── notebooks/
│   └── exploratory_analysis.ipynb
├── tests/
├── requirements.txt
├── .gitignore
└── README.md
```

*This is a suggested organization; adapt it to your existing codebase.*

## 🔬 Future Improvements

- Compare R/S Analysis with alternative Hurst Exponent estimators.
- Explore GARCH-based volatility estimates and additional market indicators.
- Benchmark Random Forest against Logistic Regression, XGBoost, and other time-series approaches.
- Add walk-forward validation and probability calibration.
- Incorporate transaction costs and backtesting to evaluate potential strategy performance.
- Analyze model stability across different assets, timeframes, and market regimes.

## ⚠️ Disclaimer

FractalQuant is an educational and research-oriented quantitative finance project. Statistical persistence does not guarantee future price direction, and machine learning predictions may fail under changing market conditions.

This project is not financial advice and should not be used for live trading without rigorous validation and risk management.

## 👨‍💻 Author

**Ishan Pandey**

B.Tech — Electronics and Communication Engineering

GitHub: [@IshanPandey32](https://github.com/IshanPandey32)

---

*Exploring the intersection of fractal statistics, financial time series, and machine learning.*