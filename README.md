# 🚚 Porter Delivery Time Prediction

**Porter** is India's largest marketplace for intra-city logistics. With over 5 million customers and 150,000+ delivery partners, Porter collaborates with restaurants to streamline food delivery logistics.

This project focuses on building a **regression model using neural networks** to estimate **delivery time** based on order and delivery partner data. Accurate delivery time predictions help improve customer satisfaction and resource management.

---

## 📁 Dataset Description

Each row in the dataset corresponds to a unique delivery and contains the following features:

| Column | Description |
|--------|-------------|
| `market_id` | Market identifier where the restaurant is located |
| `created_at` | Timestamp when the order was placed |
| `actual_delivery_time` | Timestamp when the order was delivered |
| `store_primary_category` | Category of the restaurant |
| `order_protocol` | How the order was placed (e.g. Porter app, third party) |
| `total_items` | Final price of the order |
| `num_distinct_items` | Number of unique items in the order |
| `min_item_price` | Price of the cheapest item |
| `max_item_price` | Price of the costliest item |
| `total_onshift_partners` | Number of partners on shift at the time |
| `total_busy_partners` | Number of busy partners at that time |
| `total_outstanding_orders` | Total number of pending orders |
| `estimated_store_to_consumer_driving_duration` | Estimated drive time from store to customer |

---

## 🎯 Problem Statement

Estimate the **delivery time (in minutes)** for each order based on available metadata. This can help:
- Provide customers with more accurate delivery time estimates
- Improve partner allocation
- Reduce delays and cancellations

---

## 🧠 Project Steps

### ✅ 1. Data Preprocessing & Feature Engineering
- Created target column: `delivery_time_minutes = actual_delivery_time - created_at`
- Extracted hour of day and day of week from timestamps
- Handled null values
- Encoded categorical features (`store_primary_category` and `order_protocol`)

### ✅ 2. Data Visualization & Cleaning
- Used countplots and scatterplots to explore feature distributions
- Identified and removed outliers
- Compared data before and after cleaning

### ✅ 3. Model Training
- Scaled data using MinMaxScaler
- Split into training and test sets
- Built and trained multiple **Neural Network architectures** using Keras
- Optimized using different hyperparameters, activation functions, and optimizers

### ✅ 4. Evaluation Metrics
- Used the following regression metrics:
  - **MAE**: Mean Absolute Error
  - **MSE**: Mean Squared Error
  - **RMSE**: Root Mean Squared Error

---

## 📊 Results & Insights

- Feature importance revealed that:
  - `estimated_store_to_consumer_driving_duration`
  - `total_outstanding_orders`
  - `store_primary_category`
  
  were key predictors of delivery time.

- Neural network outperformed baseline regressors after hyperparameter tuning.

---

## ❓ Leading Questions Answered

### 1. What pandas datetime functions were useful?
- `.dt.hour` → Extracts hour from datetime
- `.dt.dayofweek` → Extracts weekday
- `.dt.total_seconds()` → Converts timedelta to seconds

### 2. Why check for outliers?
Outliers skew model learning and hurt generalization. They were removed using:
- Z-score filtering
- IQR method
- Visual inspection

### 3. Classical ML alternatives
- Linear Regression
- Random Forest Regressor
- Gradient Boosting

### 4. Why scaling for Neural Nets?
Neural nets perform better when features are in similar ranges (0-1 or -1 to 1). It speeds up convergence and avoids exploding gradients.

### 5. Optimizer used
- **Adam**: Adaptive learning rate, good for noisy and sparse data.

### 6. Activation Function
- **ReLU** for hidden layers due to simplicity and effectiveness.
- **Linear** for output layer to handle regression values.

---

## 🔧 Tech Stack

- Python 🐍
- Pandas & NumPy
- Matplotlib & Seaborn
- Scikit-learn
- TensorFlow / Keras

---

## 🚀 Future Improvements

- Include geospatial data if available (e.g., customer/store coordinates)
- Add weather and traffic data as external features
- Use ensemble models for better prediction accuracy

---

## 📁 Repository Structure

```bash
Porter-Delivery-Time/
│
├── data/                     # Raw dataset files
├── notebooks/                # Jupyter notebooks
├── models/                   # Saved model files
├── plots/                    # Visualizations
├── porter_nn_model.py        # Final NN model code
├── requirements.txt          # Required Python packages
└── README.md                 # You're here!
