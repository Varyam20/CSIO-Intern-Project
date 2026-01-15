# 🌾 Crowdsourcing-Based Pest Surveillance System

## 📌 Project Overview
This project is inspired by the research paper:

> **“What a Million Indian Farmers Say?: A Crowdsourcing-Based Method for Pest Surveillance”**

The goal of this project is to explore how **crowdsourced farmer queries**, collected via government helplines, can be used as a **real-time, low-cost, and scalable alternative** to traditional pest monitoring systems.

Instead of relying on expensive sensors or satellite imagery, this approach treats **farmers themselves as distributed sensors**, enabling early detection and forecasting of pest outbreaks across large geographical regions.

---

## 🔴 Problem Statement
Crop pests are responsible for **20–40% of global agricultural losses**.  
Traditional pest detection techniques such as:

- Sensors  
- Satellite imagery  
- Cameras  
- IoT-based systems  

are often:
- Expensive  
- Difficult to deploy at national scale  
- Limited in spatial and temporal coverage  

There is a strong need for a **scalable, economical, and high-resolution pest surveillance system**.

---

## 💡 Key Idea
Farmers already report pest-related issues through **government-run helplines**.

👉 **Core Insight:**  
These farmer queries can be repurposed as **crowdsourced, real-time pest surveillance data**.

This transforms routine helpline interactions into a **nationwide monitoring system**.

---

## 🟢 What is Crowdsourcing?
Crowdsourcing refers to **collecting data from a large group of people instead of physical sensors**.

### Examples:
- Google Maps traffic data (from users’ phones)  
- Twitter data for disaster detection  
- **This project:** Farmers’ phone calls  

### Why crowdsourcing works here:
- Millions of farmers participate naturally  
- Zero additional data collection cost  
- Real-time information  
- Nationwide coverage  
- High spatial granularity (state / district / block level)  

---

## 📞 Data Source: Kisan Call Center (KCC)

### What is KCC?
- A government-run agricultural helpline  
- Farmers call to report problems or seek advice  
- Queries are answered by agricultural experts  

### Dataset Characteristics:
- **10.9 million queries**
- Time span: **2015–2020**
- Coverage: **31 states, 553 districts**

### Each query contains:
| Field | Description |
|------|------------|
| Crop | Crop type |
| Query Text | Farmer’s question |
| Answer | Expert response |
| Pest Info | Mentioned or not |
| Location | State, district, block |
| Time | Date & time |

This makes the dataset **spatio-temporal** in nature.

---

## 🧹 Data Cleaning & NLP Preprocessing

### Challenges:
- Multiple regional languages  
- Spelling mistakes  
- Code-mixed text (Hindi + English)  
- Missing or incomplete entries  

### Preprocessing Steps:
- Remove incomplete records  
- Translate queries to English (Google Translate API)  
- Spell correction (TextBlob)  
- Text normalization  

These steps are essential to make the data suitable for **analysis and modeling**.

---

## 🟢 Pest Query Identification (Labeling)

To identify pest-related queries:
- A dictionary of pest names was created  
- One-character spelling variations were allowed  
- Pest names were searched in:
  - Farmer queries **or**
  - Expert responses  

### Result:
- **867,337 pest-related queries**
- Approximately **7.9% of total queries**

---

## 🟢 Normalization of Pest Frequency

### Why normalization is needed:
Different regions vary significantly in:
- Cultivated land area  
- Number of farmers  

### Conceptual Formula:
Normalized Pest Frequency =(Number of pest-related queries) ÷ (Gross cultivated area of the district)

### Benefits:
- Enables fair comparison across regions  
- Removes bias toward larger states or districts  

---

## 🗺️ Spatio-Temporal Analysis

### Spatial Analysis:
- Identifies **where** pest outbreaks occur  

### Temporal Analysis:
- Identifies **when** pests appear  
- Helps detect seasonal trends  

### Key Observation:
Pest query spikes closely matched **real-world pest outbreaks** reported later in newspapers.

⚠️ **Important Insight:**  
KCC data detected pest outbreaks **1–2 months earlier** than news reports, demonstrating strong real-world validity.

---

## 📈 Time Series Analysis

Pest query data is treated as **time series data**, enabling:
- Trend analysis  
- Seasonality detection  
- Forecasting  

### Example:
Day 1 → 10 pest queries
Day 2 → 15 pest queries
Day 3 → 9 pest queries

---

## 🔁 Seasonality Detection (Autocorrelation)

Autocorrelation measures how a time series correlates with its **past values**.

### Observed Seasonal Patterns:
| Pest | Seasonality |
|------|------------|
| Whitefly | Yearly |
| Bug | Yearly |
| Aphid | Half-yearly |
| Stemborer | Half-yearly |

This confirms that pest populations follow **biological and agricultural cycles**.

---

## 🧪 Stationarity & Dickey–Fuller Test

### Why stationarity matters:
Most time-series forecasting models assume:
- Constant mean  
- Constant variance  
- No long-term trend  

### Dickey–Fuller Test:
- Used to test stationarity  
- **p-value < 0.05 → Stationary**  

If data is non-stationary:
- Log transformation is applied  
- Differencing is performed  

### Differencing Formula:
yₜ = yₜ − yₜ₋ₙ

---

## 🤖 SARIMA Model (Forecasting)

### SARIMA = Seasonal ARIMA

| Parameter | Meaning |
|---------|--------|
| p | Autoregressive order |
| d | Differencing order |
| q | Moving average order |
| P, D, Q | Seasonal counterparts |
| S | Seasonal length |

### Why SARIMA?
- Handles trend, seasonality, and noise  
- Well-suited for agricultural time-series data  

---

## 🧠 Model Training & Evaluation

### Training Pipeline:
1. Split data:
   - 70% training  
   - 30% testing  
2. Grid search for optimal parameters  
3. Model selection using **AIC (Akaike Information Criterion)**  
   - Lower AIC = better trade-off between accuracy and complexity  
4. Forecast future pest activity  

### Evaluation Metrics:
- RMSE (Root Mean Square Error)  
- Mean Standard Error  
- Confidence Intervals  

---

## 📊 Results & Impact

### Model Capabilities:
- Predicts pest arrival time  
- Estimates duration of infestation  
- Captures severity trends  

### Practical Benefits:
- Farmers apply pesticides **only when necessary**  
- Government agencies receive **early warnings**  
- Reduced crop loss  
- Improved food security  

---

## ✅ Key Contributions
- Scalable nationwide solution  
- Low-cost and data-driven  
- High spatial and temporal resolution  
- Real-world validated using historical outbreaks  

---

## 🚀 Future Work
- Integrating weather and climate data  
- Comparing SARIMA with LSTM / Prophet models  
- Deploying a real-time dashboard for pest alerts  
