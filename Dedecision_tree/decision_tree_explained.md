# 🌳 Decision Tree Explained (with Salary Prediction Example)

## 1. What is a Decision Tree?
A **Decision Tree** is a supervised machine learning algorithm that makes predictions by breaking down a complex decision into a series of simple **if-else conditions** (rules).

It mimics human decision-making and resembles an upside-down tree:
- **Root Node:** The starting question with the most predictive power.
- **Internal (Branch) Nodes:** Follow-up questions based on specific features.
- **Leaf Nodes:** The final answer/prediction (no further splits).

---

## 2. When to Use Decision Trees?
- When you want an **explainable, transparent model** (unlike black-box neural networks).
- When data contains a mix of **categorical** (e.g. company, degree) and **numerical** features.
- When patterns are **non-linear** (decision boundaries are step-like instead of straight lines).
- When you don't want to worry about **feature scaling** (trees only compare values, e.g. `x > 5`).

---

## 3. Example Dataset: `salaries.csv`

The goal is to predict **`salary_more_then_100k`** (`1` = Yes, `0` = No) based on **Company**, **Job**, and **Degree**:

| Row | Company | Job | Degree | Salary > 100k? |
|:---:|:---|:---|:---|:---:|
| 1 | `google` | `sales executive` | `bachelors` | **0** |
| 2 | `google` | `sales executive` | `masters` | **0** |
| 3 | `google` | `business manager` | `bachelors` | **1** |
| 4 | `google` | `business manager` | `masters` | **1** |
| 5 | `google` | `computer programmer` | `bachelors` | **0** |
| 6 | `google` | `computer programmer` | `masters` | **1** |
| 7 | `abc pharma` | `sales executive` | `masters` | **0** |
| 8 | `abc pharma` | `computer programmer` | `bachelors` | **0** |
| 9 | `abc pharma` | `business manager` | `bachelors` | **0** |
| 10 | `abc pharma` | `business manager` | `masters` | **1** |
| 11 | `facebook` | `sales executive` | `bachelors` | **1** |
| 12 | `facebook` | `sales executive` | `masters` | **1** |
| 13 | `facebook` | `business manager` | `bachelors` | **1** |
| 14 | `facebook` | `business manager` | `masters` | **1** |
| 15 | `facebook` | `computer programmer` | `bachelors` | **1** |
| 16 | `facebook` | `computer programmer` | `masters` | **1** |

---

## 4. Visualizing the Dataset as a Decision Tree

Notice key patterns in the table:
1. Every single person at **Facebook** makes > 100k (100% pure split!).
2. At **Google**, all `sales executive`s make $\le$ 100k, all `business manager`s make > 100k, and `computer programmer`s depend on whether they have a `masters`.
3. At **ABC Pharma**, only `business manager` with a `masters` makes > 100k.

Here is how the Decision Tree splits this data:

```
                            [ Company? ]
                           /      |     \
                          /       |      \
                         /        |       \
               facebook /   google|        \ abc pharma
                       v          v         v
                 [ Salary = 1 ]  [ Job? ]   [ Job? ]
                (100% of cases)  /   |  \    /    \
                                /    |   \  /      \
             sales exec _______/     |    \/        \ business manager
            v                        |    v          v
      [ Salary = 0 ]                 | [Salary = 0] [ Degree? ]
                                     |               /        \
                   business manager / \ programmer  /          \
                                   v   v  bachelors/            \ masters
                        [ Salary = 1 ] [ Degree? ] v             v
                                       /        \ [ Salary = 0 ] [ Salary = 1 ]
                            bachelors /          \ masters
                                     v            v
                               [ Salary = 0 ]  [ Salary = 1 ]
```

---

## 5. How the Algorithm Builds the Tree: Gini Impurity & Entropy

At each step, the tree tests all possible questions and picks the one with the highest **purity**:

- **Gini Impurity:** Measures the likelihood of an incorrect classification.
  $$\text{Gini} = 1 - \sum p_i^2$$
  - $\text{Gini} = 0.0 \implies$ Pure node (all items belong to one class).
  - The feature split with the lowest weighted Gini impurity becomes the next node.

---

## 6. Next Implementation Steps in Python
1. **Encode text columns to numbers** using `sklearn.preprocessing.LabelEncoder`.
2. Train the model using `DecisionTreeClassifier()`.
3. Visualize the learned tree using `tree.plot_tree()`.
