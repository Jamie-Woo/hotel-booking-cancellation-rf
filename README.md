dataset : https://www.kaggle.com/c/airbnb-recruiting-new-user-bookings/data

# 🏨 Hotel Booking Cancellation Analysis

A machine learning project that analyzes hotel booking data to predict cancellations, understand customer behavior, and identify key influencing variables.

## 📌 Objectives

This project was conducted with three main goals:

1. Predict hotel booking cancellations.
2. Analyze customer characteristics and segments.
3. Identify the most important features contributing to cancellations.

---

## 🧠 Hypotheses

### 1. Customer Behavior Hypotheses

- Hotel prices are higher during the peak vacation season (July–August).
- Resort hotels attract more visitors than city hotels.
- Short-stay customers prefer resort hotels, long-stay customers prefer city hotels.

### 2. Modeling Hypotheses

- The most influential variable in cancellation is the number of previous cancellations.
- Random Forest will outperform XGBoost on this dataset.

---

## 📊 Data Description & Preprocessing

### 🧾 Dataset Features
- Booking information (lead time, booking changes, previous cancellations, etc.)
- Hotel type and pricing
- Customer preferences and requests

### 🧹 Preprocessing Steps

- Removed irrelevant columns (e.g., arrival details, customer name).
- Applied one-hot encoding to categorical features.
- Filled missing values with column means.
- No normalization needed for tree-based models.

---

## ⚙️ Model Selection & Justification

We selected **Random Forest** and **XGBoost**, two ensemble learning algorithms, based on their robustness and suitability for high-dimensional, non-linear data.

### 🔹 Random Forest
- Reduces overfitting
- Suitable for both regression & classification
- Handles missing values effectively

### 🔸 XGBoost
- Incorporates regularization and pruning
- Excellent performance on imbalanced data
- Fast and efficient for large datasets

---

## ✅ Final Model: Random Forest

### 🔧 Hyperparameter Tuning

Used `GridSearchCV` with the following search space:

- `n_estimators`: [100, 200, 300, 400, 500]
- `criterion`: ['gini', 'entropy']

### 🏆 Best Model Parameters

| Parameter | Value        |
|-----------|--------------|
| Model     | Random Forest |
| Estimators | 400         |
| Criterion | gini         |
| Accuracy  | ~0.903       |

### 📈 Learning Curve Analysis

- Training score plateaued, suggesting a complexity limit of the Random Forest model.
- Bias decreases and variance remains stable as model complexity increases — indicating good generalization.

---

## 🔍 Feature Importance & PDP (Partial Dependence Plot)

### 💡 Top 10 Features

| Feature                      | Description                                        |
|-----------------------------|----------------------------------------------------|
| `lead_time`                 | Days between booking and check-in                 |
| `adr`                       | Average daily rate                                |
| `deposit_type_Non_Refund`   | Non-refundable deposit                            |
| `deposit_type_No_Deposit`   | No deposit required                               |
| `total_of_special_requests` | Total number of special requests                  |
| `stays_in_week_nights`      | Nights stayed during weekdays                     |
| `previous_cancellations`    | Number of previous cancellations                  |
| `stays_in_weekend_nights`   | Nights stayed during weekends                     |
| `booking_changes`           | Number of booking changes                         |
| `market_segment_Online TA`  | Booking made via online travel agency             |

### 📊 PDP Insights

- **lead_time**: Longer lead time → higher cancellation probability.
- **adr**: Higher prices → higher likelihood of cancellation.
- **special_requests**: More requests → lower cancellation probability.
- **week_night_stays**: Longer weekday stays → more uncertainty.
- **previous_cancellations**: Early cancellations have high impact; impact plateaus later.
- **booking_changes**: Customers with zero changes are more likely to cancel.

---

## 💼 Business Recommendations

Based on analysis, we suggest the following:

1. **Send reminder messages** to long lead-time customers to confirm intent.
2. **Offer discounts or loyalty points** to reduce cancellations from high-risk customers.
3. **Actively manage repeat cancellers** with stricter deposit/cancellation policies.
4. **Use booking change status** as a key signal: no change = higher risk.
5. **Survey customers with zero booking changes** to reduce uncertainty and offer personalized service.

---

## 🔧 Future Improvements

- Tried aggregating one-hot encoded `reservation_status_date` (year/month) for global importance but failed to implement.
- In future work, we suggest using **Shapley values** or **grouped feature importance** methods to better handle such temporal variables.

---

## 🙏 Acknowledgments

This project was conducted as part of a statistical machine learning course. It served as a valuable experience in applying real-world data science techniques to business problems.

