# Population Trends Analysis & Forecasting

A machine learning toolkit for analysing and predicting demographic changes using UN population data. This project combines statistical forecasting methods with modern ML algorithms to help researchers and policymakers understand population dynamics.

## Overview

This toolkit processes UN population datasets and applies multiple forecasting approaches including linear trends, polynomial fitting, exponential smoothing, and ensemble methods like Random Forest and XGBoost. The system automatically handles data cleaning, regional categorisation, and generates comprehensive visualisations.

## Features

- Multiple forecasting approaches (linear, polynomial, exponential smoothing)
- Machine learning models for population density prediction
- Scenario analysis with configurable growth parameters
- Automated data cleaning for UN statistical formats
- Regional analysis and comparative visualisations
- Fallback options when optional dependencies are unavailable

## Requirements

### Core Dependencies
```
pandas
numpy
matplotlib
seaborn
scikit-learn
scipy
```

### Optional Dependencies
```
xgboost          # Automatically falls back to Gradient Boosting
statsmodels      # Automatically falls back to polynomial methods
```

## Installation

1. Clone or download this repository
2. Install core dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
```

3. Optionally install enhanced features:
```bash
pip install xgboost statsmodels
```

## Data Setup

The script works with UN population data in CSV format. Update the file path in the script:

```python
FILE_PATH = r'your/path/to/population_data.csv'
```

Expected data format:
- Country/region identifiers
- Year columns
- Population estimates (mid-year, in millions)
- Population density values
- Standard UN Statistical Yearbook structure

## Usage

### Basic Analysis

Run the complete analysis pipeline:
```python
results = run_full_analysis()
```

This will:
- Load and clean your data
- Build multiple forecasting models
- Generate performance metrics
- Run scenario analyses for major countries
- Store results for further exploration

### Visualizations

Create trend plots for specific countries:
```python
plot_country_trends(results['data'], ['China', 'India', 'Brazil', 'Nigeria'])
```

Generate forecasting comparisons:
```python
plot_forecasts(results['data'], 'India', years_ahead=15)
```

### Individual Forecasting Methods

Linear trend projection:
```python
forecast = simple_trend_forecast(data, 'Nigeria', years_ahead=10)
```

Polynomial curve fitting:
```python
poly_forecast = polynomial_forecast(data, 'Brazil', years_ahead=10, degree=2)
```

Exponential smoothing (requires statsmodels):
```python
exp_forecast = exponential_smoothing_forecast(data, 'China', years_ahead=10)
```

### Machine Learning Models

Random Forest for density prediction:
```python
rf_model = build_random_forest_model(modeling_data)
print(f"Model RMSE: {rf_model['rmse']:.2f}")
```

XGBoost with automatic fallback:
```python
xgb_model = build_xgboost_model(modeling_data)
```

### Scenario Planning

Define multiple growth scenarios:
```python
scenarios = {
    'conservative': -0.01,
    'baseline': 0.0,
    'optimistic': 0.005
}

projections = scenario_analysis(data, 'Ethiopia', base_growth_rate=0.025, scenarios)
```

## Key Functions Reference

**Data Processing:**
- `load_and_clean_data()` - Handles UN data format irregularities
- `prep_data_for_modeling()` - Creates analysis-ready dataset

**Forecasting:**
- `simple_trend_forecast()` - Linear extrapolation
- `polynomial_forecast()` - Higher-order curve fitting
- `exponential_smoothing_forecast()` - Time series smoothing

**Machine Learning:**
- `build_random_forest_model()` - Ensemble method for density prediction
- `build_xgboost_model()` - Gradient boosting with fallback handling
- `build_gradient_boosting_model()` - Alternative ensemble method

**Analysis:**
- `scenario_analysis()` - Multi-scenario demographic projections
- `plot_country_trends()` - Historical visualization
- `plot_forecasts()` - Forecast method comparison

## Project Structure

```
project/
├── population_analysis.py    # Main script
├── README.md                # Documentation
├── requirements.txt         # Dependencies
└── data/                   # Data directory
    └── population_data.csv  # UN dataset
```

## Performance Metrics

The toolkit provides several evaluation measures:

- **Mean Absolute Error (MAE)** - Average prediction deviation
- **Root Mean Square Error (RMSE)** - Penalizes larger errors more heavily
- **R-squared** - Proportion of variance explained by trend models
- **Feature Importance** - Relative influence of demographic variables

## Regional Categories

Countries are automatically grouped into regions for comparative analysis:

- **Asia:** China, India, Japan, Indonesia, Philippines, Vietnam, Thailand, South Korea, Malaysia
- **Europe:** Germany, France, United Kingdom, Italy, Spain, Poland, Ukraine, Netherlands, Belgium
- **Africa:** Nigeria, Ethiopia, Egypt, South Africa, Kenya, Uganda, Algeria, Morocco, Ghana
- **Americas:** United States, Brazil, Mexico, Canada, Argentina, Colombia, Peru, Venezuela, Chile
- **Other:** Remaining countries not in predefined categories

## Configuration Options

Adjust key parameters in the script:

```python
# Forecast horizon
years_ahead = 10

# Model hyperparameters
n_estimators = 100
max_depth = 6
learning_rate = 0.1

# Data filtering
min_year = 1990
```

## Troubleshooting

**File path issues:** Verify the `FILE_PATH` variable points to your data file location.

**Encoding problems:** The script tries UTF-8 and Latin-1 automatically. For other encodings, modify the `load_and_clean_data()` function.

**Missing packages:** Core functionality works without optional dependencies. Install `xgboost` and `statsmodels` for enhanced features.

**Data format errors:** Ensure your data follows UN statistical conventions with proper country names, years, and indicator columns.

**Memory issues:** For large datasets, consider filtering to specific regions or time periods.

## Limitations

- Forecasting accuracy depends on historical data quality and length
- Regional categorisations are simplified approximations
- Long-term projections should be interpreted cautiously
- Model performance varies by country and data availability

## Contributing

This project welcomes contributions. Areas for enhancement include:

- Additional forecasting algorithms
- Improved regional classification systems
- Enhanced visualisation options
- Better handling of missing data
- Performance optimisations for large datasets

## Data Sources

Compatible with UN Population Division datasets including:
- UN Statistical Yearbook population tables
- World Population Prospects data
- Demographic and Social Statistics
  United Nations Statistics Division. (2024). Statistical Yearbook 2024. Sixty-seventh issue: Table 1 - Population, Surface Area and Density. Department of Economic and Social Affairs, United Nations.

## License

MIT License - see LICENSE file for details.

## Acknowledgments

Built using pandas, scikit-learn, matplotlib, and other open source libraries. UN Population Division provides the underlying demographic data that makes this analysis possible.
