# Stockastic

**ML-powered stock price prediction and analysis for the Indian equity market.**

Stockastic is a multi-page Streamlit web application that combines real-time financial data retrieval with time-series forecasting. It provides comprehensive stock information dashboards and uses an autoregressive model to generate 90-day price forecasts for equities listed on the Bombay Stock Exchange (BSE) and the National Stock Exchange (NSE).

---

## Features

- **Comprehensive Stock Information** -- View detailed fundamentals including market data, volume and shares, dividends and yield, valuation ratios, financial performance, cash flow, and analyst price targets.
- **Interactive Candlestick Charts** -- Explore historical price data with fully interactive Plotly candlestick charts across configurable periods (1 day to max) and intervals (1 minute to 1 month).
- **Autoregressive Price Forecasting** -- Generate 90-day forward-looking price predictions using a statsmodels AutoReg model trained on two years of daily closing prices.
- **Train/Test Visualization** -- Evaluate model fit by comparing training data, held-out test data, in-sample predictions, and out-of-sample forecasts on a single interactive chart.
- **BSE and NSE Support** -- Toggle between the Bombay Stock Exchange and National Stock Exchange for any listed equity issuer.
- **Indian Equity Coverage** -- Ships with a pre-built CSV dataset of equity issuer codes and names for streamlined stock selection via dropdown.

---

## Tech Stack

| Layer              | Technology                                          |
| ------------------ | --------------------------------------------------- |
| Frontend / UI      | Streamlit 1.33                                      |
| Data Retrieval     | yfinance 0.2.38 (Yahoo Finance API)                 |
| Forecasting Model  | statsmodels 0.14.2 (AutoReg -- autoregressive model)|
| Visualization      | Plotly 5.21, Matplotlib 3.8.4, Seaborn 0.13.2       |
| Data Processing    | pandas 2.2.2, NumPy 1.26.4, SciPy 1.13.0           |
| Language           | Python 3                                            |

---

## How It Works

1. **Stock Selection** -- The user selects an equity issuer from a dropdown populated by `data/equity_issuers.csv` and chooses either BSE or NSE. The app constructs the Yahoo Finance ticker symbol accordingly (e.g., `RELIANCE.BO` for BSE or `RELIANCE.NS` for NSE).

2. **Data Retrieval** -- The app fetches real-time stock information (fundamentals, market data, analyst targets) and historical OHLC price data from Yahoo Finance via the `yfinance` library.

3. **Stock Info Dashboard** -- The Stock Info page renders the retrieved data across organized sections: Basic Information, Market Data, Volume and Shares, Dividends and Yield, Valuation and Ratios, Financial Performance, Cash Flow, and Analyst Targets.

4. **Historical Chart** -- The Stock Prediction page renders an interactive candlestick chart for the user-selected period and interval.

5. **Model Training** -- Two years of daily closing prices are retrieved and split 90/10 into training and test sets. An autoregressive model (`AutoReg`) with a lag of 250 trading days is fitted on the training data using heteroskedasticity-consistent standard errors (`HC0`).

6. **Forecasting** -- The trained model generates predictions over the test period and then extends the forecast 90 days beyond the last available data point. Results are plotted as overlaid line traces (train, test, predictions, forecast) on an interactive Plotly chart.

---

## Project Structure

```
stockastic/
|-- .gitignore
|-- LICENSE.txt
|-- README.md
|-- requirements.txt
|-- data/
|   |-- equity_issuers.csv          # Equity issuer codes and names (BSE/NSE)
|-- analysis/
|   |-- yfinance_testing.ipynb      # Jupyter notebook for data exploration
|-- streamlit_app/
|   |-- 00_Main.py                  # Main landing page (app overview)
|   |-- helper.py                   # Shared functions: data fetching, model training
|   |-- pages/
|       |-- 01_Stock_Info.py        # Stock fundamentals dashboard
|       |-- 02_Stock_Prediction.py  # Historical charts and price forecasting
```

---

## Getting Started

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- An active internet connection (required for fetching live market data)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/akshay1389/stockastic.git
   cd stockastic
   ```

2. **Create and activate a virtual environment** (recommended)

   ```bash
   python -m venv venv
   source venv/bin/activate        # macOS / Linux
   venv\Scripts\activate           # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

### Running the Application

```bash
cd streamlit_app
streamlit run "00_Main.py"
```

The application will launch in your default browser at `http://localhost:8501`.

---

## Usage

1. **Main Page** -- Read about the project, its architecture, key features, and roadmap.

2. **Stock Info** -- Use the sidebar to select a stock from the dropdown and choose an exchange (BSE or NSE). The page displays comprehensive fundamental data organized into clearly labeled sections.

3. **Stock Prediction** -- Select a stock, exchange, time period, and data interval from the sidebar. The page renders:
   - A candlestick chart of historical OHLC prices for the selected configuration.
   - An autoregressive forecast chart showing training data, test data, in-sample predictions, and a 90-day forward forecast.

---

## Future Enhancements

- Integrate more advanced forecasting models such as LSTM and Prophet for improved prediction accuracy.
- Add quantitative trading strategy backtesting and signal generation.
- Implement portfolio optimization and tracking capabilities.
- Expand fundamental data coverage with earnings reports, balance sheets, and income statements.
- Introduce a user account system for saving watchlists and custom configurations.
- Add support for international stock exchanges beyond BSE and NSE.

---

## License

This project is licensed under the **MIT License**. See [LICENSE.txt](LICENSE.txt) for details.
