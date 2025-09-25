# Pivot Point Calculator

A comprehensive Python application for calculating pivot points in trading with both command-line and GUI interfaces. Supports multiple pivot point calculation methods commonly used in technical analysis.

## Features

- **Multiple Calculation Methods**: Classic, Woodie, Camarilla, Fibonacci, and DeMark pivot points
- **Dual Interface**: Command-line API and user-friendly Tkinter GUI
- **Batch Processing**: Calculate pivot points for multiple periods using pandas DataFrames
- **Export Functionality**: Save results to JSON format
- **Color-coded Results**: Visual distinction between support, resistance, and pivot levels
- **Input Validation**: Comprehensive error handling and user feedback

## Installation

### Prerequisites
- Python 3.6 or higher
- Required packages:
  ```bash
  pip install pandas
  ```

### Clone Repository
```bash
git clone https://github.com/AMIA322002/pivot-point-calculator.git
cd pivot-point-calculator
```

## Quick Start

### GUI Application
Run the graphical interface:
```bash
python pivot_gui.py
```

### Command Line Usage
```python
from pivot_calculator import PivotCalculator

# Initialize calculator
calc = PivotCalculator()

# Calculate pivot points
pivots = calc.calculate_pivot_points(
    high=150.50, 
    low=148.20, 
    close=149.80, 
    open_price=149.00,  # Optional for some methods
    method='classic'
)

print(pivots)
# Output: {'PP': 149.50, 'R1': 150.80, 'R2': 151.80, 'R3': 153.10, 'S1': 148.20, 'S2': 147.20, 'S3': 145.90}
```

## Pivot Point Methods

### 1. Classic Pivot Points
- **Formula**: PP = (High + Low + Close) / 3
- **Use Case**: Most commonly used, good for intraday trading
- **Levels**: PP, R1-R3, S1-S3

### 2. Woodie's Pivot Points
- **Formula**: PP = (High + Low + 2×Close) / 4
- **Use Case**: Gives more weight to closing price
- **Requirements**: Opening price required

### 3. Camarilla Pivot Points
- **Formula**: Uses multipliers (1.1/12, 1.1/6, 1.1/4, 1.1/2)
- **Use Case**: Provides closer support/resistance levels, good for range-bound markets
- **Levels**: PP, R1-R4, S1-S4

### 4. Fibonacci Pivot Points
- **Formula**: Uses Fibonacci retracement levels (38.2%, 61.8%, 100%)
- **Use Case**: Popular among swing traders
- **Levels**: PP, R1-R3, S1-S3

### 5. DeMark Pivot Points
- **Formula**: Conditional calculation based on open vs close relationship
- **Use Case**: Provides focused support/resistance levels
- **Requirements**: Opening price required
- **Levels**: PP, R1, S1

## GUI Interface

### Main Features
- **Input Section**: Enter OHLC data with method selection
- **Results Display**: Color-coded pivot levels
  - 🔴 Red: Resistance levels
  - 🟡 Yellow: Pivot point (bold)
  - 🟢 Green: Support levels
- **Action Buttons**: Calculate, Clear, Export, Load Sample Data
- **Method Info**: Detailed explanations of each calculation method

## Code Examples

### Single Calculation
```python
from pivot_calculator import PivotCalculator

calc = PivotCalculator()

# Classic method (most common)
classic_pivots = calc.calculate_pivot_points(152.30, 149.80, 151.20, method='classic')

# Fibonacci method
fib_pivots = calc.calculate_pivot_points(152.30, 149.80, 151.20, method='fibonacci')

# Woodie method (requires open price)
woodie_pivots = calc.calculate_pivot_points(152.30, 149.80, 151.20, 150.50, method='woodie')
```

### Batch Processing with DataFrame
```python
import pandas as pd

# Sample OHLC data
data = pd.DataFrame({
    'Date': pd.date_range('2024-01-01', periods=5),
    'Open': [100.0, 102.5, 101.8, 103.2, 102.9],
    'High': [102.8, 104.2, 103.5, 105.1, 104.8],
    'Low': [99.5, 101.2, 100.8, 102.1, 101.9],
    'Close': [102.3, 103.1, 102.4, 104.2, 103.5]
})

# Calculate pivot points for all periods
result = calc.calculate_multiple_periods(data, method='classic')
print(result)
```

## API Reference

### PivotCalculator Class

#### `calculate_pivot_points(high, low, close, open_price=None, method='classic')`
Calculate pivot points for a single period.

**Parameters:**
- `high` (float): Previous period's high price
- `low` (float): Previous period's low price  
- `close` (float): Previous period's closing price
- `open_price` (float, optional): Previous period's opening price
- `method` (str): Calculation method ('classic', 'woodie', 'camarilla', 'fibonacci', 'demark')

**Returns:**
- Dictionary containing pivot point and support/resistance levels

#### `calculate_multiple_periods(data, price_columns=None, method='classic')`
Calculate pivot points for multiple periods from a DataFrame.

**Parameters:**
- `data` (pd.DataFrame): DataFrame with OHLC data
- `price_columns` (dict): Column name mappings
- `method` (str): Calculation method

**Returns:**
- DataFrame with pivot points added

## File Structure
```
pivot-point-calculator/
│
├── pivot_calculator.py      # Core calculation engine
├── requirements.txt        # Python dependencies
├── README.md              # This file
```

## Testing

Run the test suite:
```bash
python -m pytest tests/
```

Run specific tests:
```bash
python -m pytest tests/test_calculations.py -v
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup
```bash
# Clone the repo
git clone https://github.com/yourusername/pivot-point-calculator.git
cd pivot-point-calculator

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Use Cases

### Day Trading
- Use Classic or Woodie methods for intraday support/resistance
- Calculate pivot points from the previous day's OHLC data
- Set stop-losses and profit targets based on pivot levels

### Swing Trading  
- Fibonacci pivots work well for longer-term positions
- Weekly/monthly pivot calculations for trend analysis
- Combine with other technical indicators

### Algorithmic Trading
- Integrate calculations into trading bots
- Batch process historical data for backtesting
- Export results for external analysis tools

## Known Issues

- DeMark method only provides R1/S1 levels (by design)
- GUI requires Tkinter (included in most Python installations)
- Large DataFrame processing may be memory-intensive

## Acknowledgments

- Pivot point formulas based on established trading methodologies

## Support

If you encounter any issues or have questions:

1. Check the Issue Page
2. Create a new issue with a detailed description
3. Include sample data and error messages if applicable

## Changelog

### v1.0.0 (2024-01-01)
- Initial release with all five pivot point methods
- Tkinter GUI implementation
- Batch processing capabilities
- Export functionality

---

**Happy Trading! 📈**
