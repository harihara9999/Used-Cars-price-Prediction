# 🚗 Car Price Prediction — EDA & Machine Learning

> **Can we predict the price of a car from its specs alone?**  
> This project uses exploratory data analysis and linear regression to find out — and achieves an **R² of 86.1%**.

---

## 📌 Business Problem

Car manufacturers and dealerships need accurate pricing models to stay competitive. Setting a price too high loses customers; too low erodes margin. This project builds a data-driven pricing engine using 26 vehicle attributes — from engine size and horsepower to fuel type and body style — to predict the market price of a car.

**Key question:** Which car features actually drive price, and by how much?

---

## 📊 Dataset

| Property | Detail |
|---|---|
| Source | `CarPrice_Assignment.csv` |
| Records | 205 car models |
| Features | 26 (numerical + categorical) |
| Target | `price` (USD) |
| Price range | $5,118 — $45,400 |
| Average price | $13,276 |
| Missing values | None (after cleaning) |
| Duplicates | None |

**Feature categories covered:**
- Dimensions — wheelbase, car length, width, height, curb weight
- Engine specs — engine size, horsepower, bore ratio, stroke, compression ratio, peak RPM
- Fuel & transmission — fuel type, aspiration, fuel system, drive wheel
- Body — car body type, number of doors, engine location
- Efficiency — city MPG, highway MPG

---

## 🔍 Key EDA Findings

### Price distribution
- Price is right-skewed — most cars cluster in the $5K–$15K range with a long tail of premium models
- Convertibles and hardtops command the highest average prices
- Sedan is the most popular body type by volume

### What drives price up
| Factor | Impact |
|---|---|
| Engine size | Strong positive correlation with price |
| Horsepower | Strong positive correlation |
| Curb weight | Significant — heavier cars cost more |
| Wheelbase & car length | Moderate positive effect |
| Number of cylinders | More cylinders → higher price |
| Car height | No significant impact (surprising finding) |

### Category insights
- **90%** of cars run on gas; diesel cars are rarer but command a **higher average price**
- **Turbo** aspiration cars make up only **18%** of the dataset but are priced lower on average than standard aspiration
- **56%** of cars have 4 doors; sports cars maintain similar pricing regardless of door count
- **Front-wheel drive** dominates at the lower price tier — buyers choose it for affordability
- **OHC** (overhead cam) is the most common engine type, correlating with lower prices
- **Toyota** is the most frequently appearing brand in the dataset

### Correlation highlights
- `enginesize`, `curbweight`, `horsepower` show the strongest correlations with `price`
- `citympg` and `highwaympg` are negatively correlated with price (efficient ≠ expensive)

---

## ⚙️ Methodology

### 1. Data Cleaning
- Checked and confirmed zero null values and zero duplicates
- Verified data types across all 26 columns
- Reviewed unique value counts per categorical feature

### 2. Exploratory Data Analysis
- Distribution plots for all 14 numerical features
- Count plots for 9 categorical features
- Box plots: each categorical feature vs price
- Bar charts: top 20 car models by frequency and average price
- Correlation heatmap across all numerical features

### 3. Feature Engineering
| New Feature | Formula | Rationale |
|---|---|---|
| `power_to_weight_ratio` | horsepower / curbweight | Captures performance efficiency |
| `*_squared` features | column² for each numerical feature | Captures non-linear relationships |
| `log_enginesize` | log(enginesize + 1) | Normalizes skewed engine size distribution |
| `brand` | Extracted from CarName | Brand-level pricing signal |
| `model` | Extracted from CarName | Model-level specificity |

### 4. Preprocessing
- Label encoding applied to all categorical columns
- Standard scaling applied to all numerical columns
- 80/20 train-test split (random state = 42)

### 5. Modelling
- Algorithm: **Linear Regression** (scikit-learn)
- Evaluation metrics: R² score, Mean Squared Error

---

## 📈 Model Performance

| Metric | Value |
|---|---|
| **R² Score** | **86.1%** |
| Algorithm | Linear Regression |
| Train/Test split | 80% / 20% |

The model explains **86.1% of the variance** in car prices using the engineered feature set — a strong baseline for a linear model on this dataset.

---

## 🛠️ Tech Stack

```
Python 3.x
├── pandas          — data manipulation
├── numpy           — numerical operations
├── matplotlib      — base visualizations
├── seaborn         — statistical plots
└── scikit-learn    — preprocessing, modelling, evaluation
    ├── StandardScaler
    ├── LabelEncoder
    ├── train_test_split
    ├── LinearRegression
    └── mean_squared_error / r2_score
```

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Run the notebook
```bash
git clone https://github.com/harihara9999/car-price-prediction.git
cd car-price-prediction
jupyter notebook Car_price_prediction.ipynb
```

Make sure `CarPrice_Assignment.csv` is in the same directory as the notebook before running.

---

## 📁 Project Structure

```
car-price-prediction/
│
├── Car_price_prediction.ipynb   # Main notebook (EDA + modelling)
├── CarPrice_Assignment.csv      # Dataset
└── README.md                    # This file
```

---

## 💡 Business Insights Summary

1. **Engine size is the single strongest price predictor** — manufacturers can use this as a primary pricing anchor
2. **Fuel efficiency and price move in opposite directions** — budget buyers and eco-conscious buyers are the same segment
3. **Brand extraction significantly improves prediction** — Toyota clusters at lower prices, luxury brands at higher
4. **Car height adds no pricing value** — width and length matter, height doesn't
5. **Diesel cars are niche but premium** — a smaller but higher-value market segment worth targeting separately

---

## 🔮 Potential Improvements

- Try ensemble models (Random Forest, XGBoost) to capture non-linear relationships
- Add cross-validation for more robust performance estimates
- Deploy as a Streamlit web app for interactive price prediction
- Incorporate brand reputation scores from external sources
- Experiment with polynomial regression to better capture the engine size–price curve

---

## 👤 Author

**Hari Hara Naidu**  
📧 patakanuruhariharanaidu@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/hariharanaidu/) | [GitHub](https://github.com/harihara9999)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
