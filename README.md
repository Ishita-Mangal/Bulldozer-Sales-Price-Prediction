# Blue Book for Bulldozers

## Objective

The goal of this project is to develop a regression model that accurately predicts the sale price of bulldozers and other heavy machinery at auction. This enables Fast Iron to build a reliable “Blue Book” pricing guide for its customers.

---

## Dataset Overview

The dataset includes information on:

- Equipment type and configuration
- Usage details (e.g., machine hours)
- Auction data (location, timing, auctioneer ID)
- Temporal patterns (sale dates)

### Files Used:

- `Train.csv` – Full training data with target `SalePrice`, which contains data through the end of 2011.
- `Train_valid.csv` – This dataset is split internally into training and validation sets (typically 80/20) for model evaluation using RMSLE.
- `Valid.csv` – Test set to evaluate model performance, which contains data from January 1, 2012 - April 30, 2012 You make predictions on this set
- `Test.csv` – Testing dataset for final predictions, it contains data from May 1, 2012 - November 2012.

---

## Workflow

### 1. Data Cleaning and Preprocessing

- Parsed and extracted date-based features from `saledate`
- Filled missing values:
  - Numerical: filled with median
  - Categorical/binary: filled with mode
  - Columns with >90% missing values were dropped
- Converted string/object columns to categorical numeric labels
- Created derived features like:
  - `machine_age = saleyear - YearMade`
  - Sale month, year, weekday, etc.

### 2. Model Building

The following models were trained and evaluated:

- Linear Regression
- Random Forest Regressor (selected as final model)
- (Optional: comparisons with XGBoost or other advanced models)

### 3. Evaluation

- Models were evaluated using **Root Mean Squared Logarithmic Error (RMSLE)** on internal validation split
- Final model was tested on `Test.csv` (target column not available) to generate submission predictions

### 4. Final Prediction and Export

- Applied preprocessing to the test data
- Used the final Random Forest model for prediction
- Saved predictions to `test_preds.csv`

---

## Model Performance (on internal validation)

| Model                          | RMSLE         |
| ------------------------------ | ------------- |
| Linear Regression              | ~0.40         |
| Random Forest (100 estimators) | ~0.2-0.3~ |

---

## Repository Structure

```
📁 bulldozer-price-prediction/
├── Bulldozer_SalesPrice_Prediction.ipynb       # Full project notebook
├── test_preds.csv       # Final prediction results
└── README.md
```

---

## Requirements

- Python
- pandas
- numpy
- scikit-learn
- seaborn
- matplotlib

Install via pip:

```bash
pip install pandas numpy scikit-learn seaborn matplotlib
```

---

## Author

**Ishita Mangal**  
Final Year B.Tech Student, IIT Kanpur
Data Science and Machine Learning Enthusiast

---

## Notes

- This project is for academic purposes and not deployed in production.
- RMSLE is used as the evaluation metric since it penalizes underestimations more — especially important for high-value auction items.
