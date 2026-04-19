# 📊 Cross-Sell Prediction with Temporal Modeling

A portfolio-ready machine learning case for predicting cross-sell adoption using **customer-level temporal data**.

> Since the original technical case dataset cannot be publicly shared, this repository uses a **realistic synthetic dataset** designed to preserve important business and temporal dynamics observed in real customer behavior.

---

## 🚀 Project Goal

The objective of this project is to predict:

- **who** is more likely to adopt Product B,
- **when** the best moment to approach the customer is,
- and **why** some customers present higher cross-sell propensity.

Instead of framing the challenge as a static classification task, the project models it as a **temporal supervised learning problem**, where each row represents a **customer-month** observation.

The target answers the following question:

> **Will this customer adopt Product B within the next 3 months?**

---

## 🧠 Why this project matters

Cross-sell is not only a predictive analytics problem — it is a **business prioritization problem**.

A good solution should not merely classify customers correctly.  
It should help business teams decide:

- which customers deserve attention first,
- how to allocate commercial effort,
- and when intervention is most likely to be effective.

This project was designed to reflect that perspective.

---

## 🏗️ Repository Structure

```bash
.
├── cross_sell_top1_notebook_synthetic.ipynb
├── README.md
├── linkedin_post.md
└── requirements.txt
```

---

## 📦 Synthetic Data Strategy

The original case data is confidential, so I built a synthetic dataset designed to be **substantially more realistic than simple random tabular simulation**.

The generator incorporates:

- **customer heterogeneity**
- **segment-level behavior**
- **temporal persistence**
- **usage growth over time**
- **product adoption driven by historical behavior**
- **pre-adoption behavioral acceleration**
- **missing values and incomplete horizons**

This makes the notebook publishable while preserving the analytical logic of the original challenge.

### What makes the synthetic data realistic?

Each customer has latent characteristics such as:

- maturity
- cross-sell affinity
- growth profile
- volatility profile
- segment size

Monthly product usage is then simulated with:

- autocorrelation,
- trend,
- seasonality,
- noise,
- and breadth of system usage.

Finally, Product B adoption is generated as a **probabilistic event conditional on engagement**, rather than as a random label.

---

## 🔍 Exploratory Data Analysis

The EDA investigates four main questions:

1. Is the dataset temporally consistent?
2. Is Product B adoption concentrated or gradual over time?
3. Do adopters differ from non-adopters?
4. Are there visible pre-adoption signals?

### Main findings

- Product B adoption is **not random**
- Adopters tend to show:
  - higher usage intensity
  - broader system usage
  - more mature behavioral profiles
- Usage and breadth often **increase before adoption**
- The trajectory suggests a meaningful **action window** prior to conversion

---

## ⚙️ Modeling Approach

### 1. Problem formulation
The problem is formulated as a **temporal classification task**.

Each row represents a **customer-month**, and the target indicates whether Product B will be adopted in the next 3 months.

### 2. Leakage-safe target creation
To preserve temporal integrity:

- only **pre-adoption observations** are kept,
- records without a full future horizon are removed,
- all features use only information available up to the reference month.

### 3. Feature engineering
The notebook includes temporal feature engineering such as:

- lag features
- month-over-month changes
- rolling means
- rolling standard deviations
- rolling min/max
- short-term vs medium-term trend features

### 4. Temporal validation
The model is evaluated using a **chronological split**:

- train
- validation
- test

This simulates how the model would behave in production.

---

## 🤖 Models

### Baseline
- Logistic Regression

### Main model
- LightGBM

### Hyperparameter tuning
A grid search is performed using:

- **temporal validation**
- **PR-AUC as the primary metric**

This choice is appropriate because the positive class is relatively sparse and business prioritization matters more than overall classification accuracy alone.

---

## 📈 Evaluation

The project goes beyond standard ML evaluation and includes **business-oriented metrics**.

### Statistical metrics
- ROC AUC
- PR AUC
- Brier Score
- Calibration Curve

### Business metrics
- Lift by decile
- Top-K precision
- Top-K recall
- Ranked customer prioritization

This makes the solution much closer to how a real cross-sell model would be assessed in a business environment.

---

## 💡 Business Interpretation

The solution helps answer three core business questions.

### Who should be approached?
Customers with higher predicted scores, especially those concentrated in the top-ranked deciles.

### When should they be approached?
In the months before adoption, when usage intensity and breadth begin to accelerate.

### Why are they likely to adopt?
Because their engagement signals indicate:

- greater maturity,
- broader product usage,
- and stronger functional complementarity.

---

## 🛠️ Tech Stack

- Python
- pandas
- NumPy
- scikit-learn
- LightGBM
- Plotly
- Jupyter Notebook

---

## ▶️ How to run

1. Clone this repository
2. Install dependencies
3. Open the notebook
4. Run all cells

```bash
pip install -r requirements.txt
jupyter notebook
```

---

## 📌 Key Takeaway

This project demonstrates how to turn a predictive modeling challenge into a **decision-support framework**.

By combining:

- temporal data structure
- realistic feature engineering
- robust validation
- explainability
- and business-oriented evaluation

the notebook goes beyond “model building” and becomes a practical portfolio case in **machine learning applied to business growth**.

---

## 👩‍💻 Author

**Cristiane Gea**  
Data Scientist | Econometrics | Machine Learning | Business Analytics

If this project interests you, feel free to connect or discuss similar applications in CRM, cross-sell, pricing, retention, or customer analytics.
