# 🌤️ Weather Data Analysis Project

This repository documents an exploratory data analysis (EDA) project performed on a comprehensive hourly weather dataset. The analysis uses the **Pandas** library in Python within a Jupyter Notebook environment to inspect, clean, and extract meaningful insights from the data.

## 🚀 Project Goal

The primary goal was to thoroughly explore the weather dataset, check for data quality issues (like missing values), understand the distribution of various weather metrics, and answer specific data science questions related to weather conditions, wind speed, and visibility.

## 📊 Dataset Overview

The dataset (`1. Weather Data.csv`) contains hourly weather measurements recorded over one full year (8784 records).

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| **Date/Time** | `object` | The date and time of the measurement. |
| **Temp\_C** | `float64` | Temperature in Celsius. |
| **Dew Point Temp\_C** | `float64` | Dew Point Temperature in Celsius. |
| **Rel Hum\_%** | `int64` | Relative Humidity percentage. |
| **Wind Speed\_km/h** | `int64` | Wind Speed in kilometers per hour. |
| **Visibility\_km** | `float64` | Visibility in kilometers. |
| **Press\_kPa** | `float64` | Pressure in kilopascals. |
| **Weather Condition** | `object` | A description of the weather condition (Originally named 'Weather'). |

## 🔍 Initial Data Exploration & Cleaning

The notebook begins with standard EDA checks:

* **Shape:** The dataset consists of **8784 rows** and **8 columns**.
* **Null Values:** Checked using `data.isnull().sum()` and found **no missing values** across any column.
* **Unique Values:** The `Weather` column contains **50 unique weather conditions**.
* **Renaming:** The column `Weather` was successfully renamed to **`Weather Condition`** using `data.rename()`.

## 📈 Key Analysis Questions & Results

The following questions were addressed and solved using Pandas indexing, aggregation, and boolean filtering:

### 1. Unique Wind Speeds

**Question:** Find all the unique 'Wind Speed' values in the data.
**Code:** `data['Wind Speed_km/h'].unique()`
**Result:** 34 unique speeds, including `0` up to a maximum recorded speed of `83 km/h`.

### 2. Frequency of 'Clear' Weather

**Question:** Find the number of times when the weather was exactly 'Clear'.
**Code:** `data['Weather Condition'].value_counts()` or `data[data['Weather Condition'] == 'Clear'].shape`
**Result:** **1326 times**.

### 3. Wind Speed of 4 km/h

**Question:** Find the number of times when the wind speed was exactly 4 km/h.
**Code:** `data.groupby('Wind Speed_km/h').get_group(4)`
**Result:** **474 times**.

### 4. Mean of Visibility

**Question:** Find the mean of 'Visibility\_km'.
**Code:** `data['Visibility_km'].mean()`
**Result:** **27.66 km**.

### 5. Standard Deviation and Variance

**Question:** What is the standard deviation of pressure and the variance of relative humidity?
**Code:** `data['Press_kPa'].std()` and `data['Rel Hum_%'].var()`
**Result:**
* **Pressure Std Dev:** 0.844 kPa
* **Relative Humidity Variance:** 286.25 (Indicating high fluctuation)

### 6. Instances of Snow

**Question:** Find all the instances when 'Snow' was recorded (including conditions like 'Rain, Snow', etc.).
**Code:** `data[data['Weather Condition'].str.contains('Snow')]`
**Result:** **579 records** contain the word 'Snow'.

### 7. Wind Speed and Visibility Condition

**Question:** Find all instances when 'Wind Speed is above 24' **and** 'Visibility is 25'.
**Code:** `data[(data['Wind Speed_km/h'] > 24) & (data['Visibility_km'] == 25)]`
**Result:** **308 times**.

### 8. Mean Values by Weather Condition

**Question:** What is the mean value of each column against each 'Weather Condition'?
**Code:** `data.groupby('Weather Condition').mean()`
**Result:** A full aggregation table showing average metric values for all 50 conditions.

---

Feel free to check out the accompanying Jupyter Notebook (`weather_analysis (1).ipynb`) for the full code and output from each step!
