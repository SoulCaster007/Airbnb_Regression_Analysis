# A Statistical Analysis of Airbnb Listing Prices in Toronto Using Multiple Linear Regression

This project investigates the key factors that influence Airbnb listing prices in Toronto using multiple linear regression. Using a dataset of more than 21,000 listings from Inside Airbnb, the analysis explores how listing characteristics such as capacity, number of bedrooms, reviews, host status, and ratings shape price variation across the city.

---

## 📁 Project Overview

Airbnb pricing is complex and influenced by many listing attributes. This project uses statistical modeling and diagnostic analysis to identify which features significantly affect price and how these effects interact.

The work includes:

- Data cleaning and preprocessing  
- Exploratory data analysis (EDA)  
- Log transformation of skewed variables  
- Polynomial and interaction terms  
- Model assumption checks and diagnostic plots  
- Robust regression to mitigate influential points  
- Interpretation of model coefficients  
- Final model comparison using R², AIC, and BIC  

---

## 📊 Dataset

**Source:** Inside Airbnb (Toronto, 2024)  
**Size:** 21,600+ listings  

**Key variables:**

- `price` (response variable, log-transformed)  
- `accommodates`  
- `bedrooms`  
- `number_of_reviews` (log-transformed)  
- `review_scores_rating`  
- `host_is_superhost` (binary)

The dataset was cleaned to remove entries with missing or invalid values (e.g., zero price, invalid ratings).

---

## 🧠 Methodology

### 1. Exploratory Data Analysis

- Visualized distributions and relationships between price and predictors  
- Identified skewness in price and review-based variables  
- Detected nonlinear patterns in `accommodates` and `bedrooms`  

### 2. Transformations & Feature Engineering

- Log-transformed `price` and `number_of_reviews`  
- Added polynomial terms for `accommodates` and `bedrooms`  
- Added interaction terms (e.g., `accommodates × bedrooms`, `log(reviews) × superhost`)  

### 3. Model Diagnostics

An initial OLS model showed:

- Violations of linearity  
- Heteroscedasticity (non-constant variance of residuals)  
- Non-normal residuals  

These issues motivated response transformation and model refinement.

### 4. Robust Regression

- Identified influential observations using Cook’s Distance  
- Applied M-estimation via robust regression (e.g., `rlm()` in R) to downweight outliers  
- Improved residual patterns and model stability without deleting data points  

---

## 📈 Final Model Performance

| Model                | Adjusted R² | AIC       | BIC       |
|----------------------|------------:|----------:|----------:|
| Initial OLS          |     ~0.366  | 142,873   | 142,919   |
| Transformed OLS      |     ~0.420  | -20,404   | -20,351   |
| **Final robust model** | **~0.452** | **-20,423** | **-20,331** |

### Key Findings

- Price increases with `accommodates` and `bedrooms`, but with **diminishing returns** (negative quadratic terms).  
- Listings with higher `review_scores_rating` tend to charge higher prices.  
- `host_is_superhost` alone is associated with slightly lower base prices, but:  
  - The interaction `log(number_of_reviews) × host_is_superhost` is positive and significant, indicating that **Superhosts with many reviews can charge more**.  
- A higher `accommodates / (bedrooms + 1)` ratio is associated with higher prices, suggesting the value of efficient use of space.

---

## 📝 Practical Insights

For **hosts**:

- Efficient space usage (more guests per bedroom) can justify higher prices.  
- Superhost status becomes especially valuable when combined with a high number of reviews.  
- Maintaining high review scores has a measurable positive impact on price.

For **platforms / analysts**:

- Pricing models should incorporate nonlinear and interaction effects, not just simple linear relationships.  
- Robust statistical methods help prevent outliers (e.g., luxury listings, data errors) from distorting recommendations.

---

## 🔧 Tools & Technologies

- **Language:** R  
- **Packages:**  
  - `tidyverse` – data wrangling & visualization  
  - `ggplot2` – EDA & diagnostic plots  
  - `MASS` – robust regression (`rlm()`)  
- **Methods:**  
  - Multiple linear regression  
  - Polynomial regression  
  - Interaction effects  
  - Robust regression (M-estimation)  
  - Residual and influence diagnostics  

---

## 📂 Project Structure

```text
/
├── data/          # Raw and cleaned Airbnb datasets
├── code/          # R scripts for EDA, modeling, diagnostics
├── figures/       # Plots (EDA, residuals, Q–Q, etc.)
├── report/        # Final project report (PDF)
└── README.md      # Project overview (this file)
