# qrt-data-challenge-2025
# QRT Illiquid–Liquid Asset Mapping Challenge  

## 🏆 Achievements  
- Reached **finalist stage** of the QRT Challenge.  
- Feature engineering to handle the data effectively
- Improved interpretability of mapping by incorporating **sector/industry metadata**.  
- Successfully scaled multi-output regression to **200k+ samples across 2748 days**.  

## 📌 Project Overview  
This repository contains my solution for the **Qube Research & Technologies (QRT) Data Challenge**.  
The objective was to **map illiquid asset returns to liquid asset returns** and predict the **signs of returns** for 100 liquid assets given historical data of 100 illiquid ones.  

Instead of regression, the challenge was reframed as a **classification task**, optimizing for a **custom weighted accuracy** that prioritizes correct predictions on large returns.  

---

## 🗂️ Dataset  
- **X_train.csv** – Illiquid asset returns and identifiers (`ID`, `ID_DAY`, `RET_i`, `ID_TARGET`)  
- **y_train.csv** – Target liquid asset returns (`RET_TARGET`)  
- **X_test.csv** – Test inputs for final predictions  
- **assets.csv** – Sector/industry metadata (hierarchical `CLASS_LEVEL_j`)  

---

## ⚙️ Methodology  

### 1. Data Preprocessing  
- **Missing values** handled via:  
  - Sector-level weighted imputation  
  - Class-level fallback averaging  
- **Normalization**: StandardScaler (mean=0, std=1)  
- **Filtering**: Weak signals (< 1e-5) removed to reduce noise  

### 2. Feature Engineering  
- Per-day aggregation of returns  
- Class-level embeddings of illiquid assets  
- Cross-sectional factor construction using label correlations  

### 3. Modeling Approaches  
Explored multiple families of models:  
- **Linear models**: LASSO, ElasticNet, Ridge  
- **Tree-based models**: RandomForest, XGBoost, CatBoost  
- **Gaussian Process regression** (limited by compute)   

Final pipeline:  
- **Multi-output ElasticNet with sector-weighted imputation**  
- GroupKFold validation over `ID_DAY` to avoid leakage  

---

## 📊 Results  

| Model                   | Weighted Accuracy |
|--------------------------|------------------|
| Benchmark (linear corr.) | 0.6944 |
| LASSO Regression         | ~0.7429 |
| Random Forest            | ~0.72 |
| AdaBoost                 | ~0.67 |
| ElasticNet (final)       | **~0.7489** |

✅ My solution improved the benchmark significantly (from **69% → ~75%**), achieving competitive leaderboard performance.  

---

## 📂 Repository Structure  

