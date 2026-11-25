# 🧭 How to Select the Right Machine Learning Algorithm

Choosing the best machine learning model is not about guessing; it is a systematic decision process based on **your target variable**, **feature characteristics**, **data size**, and **interpretability needs**.

---

## 1. Quick Decision Roadmap

```text
                                [ What is your Target variable (y)? ]
                                           /              \
                                          /                \
                       [ Continuous Number ]             [ Discrete Category ]
                                  |                                |
                        REGRESSION PROBLEM               CLASSIFICATION PROBLEM
                                  |                                |
               +------------------+                    +-----------+-----------+
               |                  |                    |                       |
        [ Linear Trend ]   [ Non-Linear / Rules ]   [ 2 Classes (0 / 1) ]   [ 3+ Classes ]
               |                  |                    |                       |
        Linear Regression   Decision Tree Regressor    |                Multiclass Logistic Reg.
                            Random Forest Regressor    |                Random Forest / SVM
                                                       |
                                        +--------------+---------------+
                                        |                              |
                            [ Linear / Smooth Curve ]      [ Complex Rules / Mixed Data ]
                                        |                              |
                               Logistic Regression              Decision Tree
                                                                Random Forest
```

---

## 2. The 4-Step Selection Framework

### Step 1: Identify Problem Type (Target $y$)
- **Regression:** Target is continuous (e.g. house price, salary amount, temperature).
  - *Algorithms:* Linear Regression, Ridge/Lasso, DecisionTreeRegressor, RandomForestRegressor.
- **Binary Classification:** Target has 2 classes (`0` or `1`, Yes or No, Spam or Ham).
  - *Algorithms:* Logistic Regression, DecisionTreeClassifier, SVM, Random Forest.
- **Multiclass Classification:** Target has 3+ classes (e.g., Digits 0–9, Flower species).
  - *Algorithms:* Multiclass Logistic Regression (One-vs-Rest/Softmax), Random Forest, SVM.

---

### Step 2: Check Feature Relationships (Linear vs Non-Linear)
- **Linear / Smooth S-Curve Relationship:**
  - When the probability increases smoothly as a feature grows (e.g. Age $\rightarrow$ Insurance purchase).
  - 👉 **Choose:** **Logistic Regression** (lightweight, interpretable, low risk of overfitting).
- **Rule-Based / Step-wise / Non-Linear Interactions:**
  - When decisions depend on conditional rules (e.g. Titanic: *"Women and children survived, but if male, only 1st class survived"*).
  - 👉 **Choose:** **Decision Tree** or **Random Forest**.

---

### Step 3: Check Data Types & Preprocessing Requirements

| Property | Linear / Logistic Regression | Decision Trees / Random Forests |
| :--- | :--- | :--- |
| **Feature Scaling** | **Required** (Features on different scales distort gradient descent) | **Not needed** (Only checks threshold `feature > value`) |
| **Outliers** | **Sensitive** (Extreme values pull the line/boundary) | **Immune** (Only cares about rank/order of values) |
| **Mixed Features** | Needs one-hot encoding, scaling, normalization | Handles mixture of numbers and encoded categories naturally |
| **Interpretability** | Moderate (Coefficients/weights) | **High** (You can literally plot and read the tree) |

---

### Step 4: Dataset Size & Overfitting Risk
- **Small Datasets (< 50 rows):**
  - High risk of overfitting. Use simple models, or Decision Trees with low `max_depth` (e.g. depth 2 to 4).
- **Medium to Large Tabular Datasets (1,000+ rows):**
  - **Random Forest** or **Gradient Boosting (XGBoost/LightGBM)** are industry gold standards for tabular data.
- **High-Dimensional Data (e.g., Images, Pixels, Text):**
  - **SVM**, Logistic Regression, or Neural Networks perform best.

---

## 3. Algorithm Cheat Sheet (When to Pick What)

| Algorithm | Best Used When... | Avoid When... |
| :--- | :--- | :--- |
| **Linear Regression** | Target is a continuous number with linear feature trends. | Relationships are non-linear or feature interactions are complex. |
| **Logistic Regression** | Target is binary/multiclass with smooth decision boundaries; speed & probability confidence matter. | Features have heavy non-linear interactions without manual feature engineering. |
| **Decision Tree** | You need complete explainability; data has mixed categorical/numeric columns and if-else rules (e.g. Titanic). | The tree grows too deep and overfits without pruning (`max_depth`). |
| **Random Forest** | You want the highest possible accuracy on tabular data without tuning many parameters. | You need to explain the exact decision path to non-technical stakeholders (it's an ensemble of 100+ trees). |
| **Support Vector Machine (SVM)** | Complex classification boundaries in medium-sized, clean datasets (like digit/character recognition). | Dataset is huge (training time becomes very slow) or noisy with overlapping classes. |

---

## 4. Why Titanic is Best for a Decision Tree
- **Mixed Data:** Contains continuous numbers (`Age`, `Fare`), rank orders (`Pclass`), and categories (`Sex`, `Embarked`).
- **Heavy Rule-Interactions:** Survival depended on combined rules (*Gender $\times$ Class $\times$ Age*), which mirrors a tree's split hierarchy.
- **Extreme Outliers:** Passenger fares range from £0 to £512. Trees ignore this scale difference without distorting the model.
