# RobustPreprocessor

**RobustPreprocessor** is a Python package for comprehensive and flexible data preprocessing. It is designed to clean and prepare numeric datasets for machine learning and analysis by handling outliers, missing values, infinity values, and redundant features.

---

## Features

- **Outlier Handling**:
  - Interquartile Range (IQR) clipping.
  - Z-score filtering.
  
- **Infinity Value Handling**:
  - Replace with finite extremes.
  - Drop rows containing infinity.
  - Replace with a specific default value (e.g., 0).

- **Missing Value Imputation**:
  - Mean, median, or most frequent value strategies.

- **Feature Removal**:
  - Drop constant or near-constant features.
  
- **Visualization**:
  - Plot feature distributions with histograms.

- **Execution Logging**:
  - Outputs a JSON summary of preprocessing steps, including dropped columns and execution time.

---

## Installation

Install via pip:

```bash
pip install robustpreprocessor
```

Or clone the repository and install locally:

```bash
git clone https://github.com/nqmn/robustpreprocessor.git
cd robustpreprocessor
pip install .
```

---

## Usage

### Import the Package

```python
from robustpreprocessor import RobustPreprocessor
import pandas as pd

# Example dataset
data = pd.DataFrame({
    "feature_1": [1, 2, 3, 1000, 5],
    "feature_2": [1, 2, None, 4, 5],
    "feature_3": [0, 0, 0, 0, 0],
    "feature_4": [1, 2, np.inf, -np.inf, 5],
})

# Initialize the preprocessor
preprocessor = RobustPreprocessor(verbose=True)

# Preprocess the dataset
cleaned_data = preprocessor.preprocess(
    data,
    outlier_method="IQR",
    infinity_handling="set_value",
    missing_value_strategy="mean",
    feature_removal_criteria="constant"
)

# View the cleaned data
print(cleaned_data)
```

---

## Visualization

Use the `plot_feature_distributions` method to visualize the distributions of numeric features:

```python
preprocessor.plot_feature_distributions(cleaned_data)
```

---

## Logging and Execution Summary

After preprocessing, the class outputs a JSON log summarizing the steps taken, including execution time and dropped columns:

```json
{
    "process_type": "RobustPreprocessor",
    "user_selections": {
        "outlier_method": "IQR",
        "infinity_handling": "set_value",
        "missing_value_strategy": "mean",
        "feature_removal_criteria": "constant"
    },
    "steps_executed": {
        "select_numeric_columns": "Selected 4 numeric columns",
        "outlier_handling": "Handled outliers using IQR method.",
        "infinity_handling": "Replaced infinity values with a set value (0).",
        "missing_value_imputation": "Imputed missing values with mean strategy.",
        "feature_removal": "Dropped 1 constant columns."
    },
    "dropped_columns": 1,
    "execution_time_seconds": 0.1234
}
```

---

## Dependencies

- `numpy`
- `pandas`
- `scikit-learn`
- `matplotlib`
- `scipy`

Install them with:

```bash
pip install -r requirements.txt
```

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Commit your changes with clear descriptions.
4. Submit a pull request.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## Support

If you encounter issues or have questions, feel free to open an issue on [GitHub](https://github.com/nqmn/robustpreprocessor/issues).

---

## Acknowledgments

- Inspired by common challenges in data preprocessing.
- Thanks to the contributors and the open-source community!