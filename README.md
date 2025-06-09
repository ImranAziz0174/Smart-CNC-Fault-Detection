
# Smart CNC Fault Detection  
**A Data-Driven Modeling Framework for Predicting Tool Wear and Clamping Faults Using Time-Series Sensor Data**

![Python](https://img.shields.io/badge/Built%20with-Python-3776AB?logo=python&logoColor=white)  
![Machine Learning](https://img.shields.io/badge/Model-XGBoost%20%7C%20Logistic%20Regression-blueviolet)  
![Status](https://img.shields.io/badge/Project%20Status-Completed-success)  
![License](https://img.shields.io/badge/License-Academic-lightgrey)

---

## Overview
This project implements a predictive maintenance framework for CNC (Computer Numerical Control) machines, with an emphasis on early detection of **tool wear** and **clamping inadequacies**. Using high-frequency, multi-axis sensor data collected from 18 controlled milling experiments at the **System-level Manufacturing and Automation Research Testbed (SMART Lab)** at the University of Michigan, the project explores machine learning approaches for classifying fault conditions based on temporal patterns in motor current, velocity, and power signals.

A comprehensive pipeline was developed in Python, involving exploratory data analysis, multivariate signal visualization, feature extraction, and supervised classification. Both linear (Logistic Regression) and ensemble-based (XGBoost) models were benchmarked to assess their effectiveness in real-time fault prediction tasks critical to smart manufacturing.

---

## Project Structure

```
├── EDA.ipynb                        # Data distribution, correlation heatmaps, and class imbalance analysis
├── Sensor Trend.ipynb              # Visualization of time-series sensor trends (motor currents, power, velocity)
├── Logistic Regression.ipynb       # Baseline classification models for tool wear and clamping detection
├── XGBoost.ipynb                   # Non-linear modeling for performance improvement
├── XGBoost_Cross_Validation.ipynb  # Grid search and cross-validation for hyperparameter optimization
├── Comparison.ipynb                # Model benchmarking using accuracy, F1-score, and confusion matrices
├── Training Dataset.csv            # Metadata for each experiment (feedrate, clamp pressure, labels)
├── Imran Aziz - Final Report.pdf   # Full technical report detailing methodology, results, and analysis
```

---

## Dataset Description

### Source  
Data was acquired from 18 wax-block CNC machining experiments conducted at the **SMART Lab, University of Michigan**. Each experiment involved a complete machining cycle using varying parameters and captured both **metadata** and **high-frequency time-series signals**.

### A. Metadata (`Training Dataset.csv`)
- `feedrate` (mm/s): Tool’s linear speed relative to the workpiece  
- `clamp_pressure` (bar): Clamping force securing the workpiece  
- `tool_condition`: Binary classification label (worn/unworn)  
- `passed_visual_inspection`: Output quality based on visual criteria  

### B. Sensor Time-Series Data (Not uploaded publicly due to file size)
Each experiment includes over 40 columns sampled at 100ms intervals, capturing:
- Motor positions (actual and commanded)
- Velocities, accelerations
- Electrical properties: current feedback, output voltage, and spindle power
- Machining stage metadata (e.g., M1_SEQUENCE_NUMBER, LAYER labels)

---

## Modeling Approach

### 1. **Exploratory Data Analysis**
- Distribution analysis of class labels and input features  
- Correlation matrix to understand sensor interdependencies  
- Identification of dominant parameter clusters (e.g., fixed clamp pressure steps)

### 2. **Sensor Trend Analysis**
- Visualization of current, power, and velocity patterns over time across experiments  
- Comparison of signal behavior for worn vs. unworn tools to identify early degradation markers

### 3. **Feature Engineering**
- Statistical descriptors (mean, std, RMS, min, max) extracted from raw signals  
- Feature selection via Random Forest importance scores to reduce dimensionality and noise

### 4. **Modeling and Evaluation**
- **Logistic Regression**: Served as a baseline linear classifier  
- **XGBoost**: Used for capturing complex, non-linear feature interactions  
- **Grid Search with 5-Fold Cross-Validation** for hyperparameter tuning  
- Evaluated via accuracy, precision, recall, F1-score, and confusion matrices

---

## Key Findings

- **Tool Wear Prediction**:  
  - Logistic Regression: 33% Accuracy, poor recall for worn tools  
  - XGBoost: 60% Accuracy, significantly improved F1-score for 'worn' class

- **Clamping Fault Detection**:  
  - Both models achieved ~80% Accuracy  
  - Logistic Regression showed higher precision and general reliability

These results demonstrate that ensemble models like XGBoost are more robust for complex fault detection, while simpler models like Logistic Regression can still be valuable for well-separated classes with structured inputs.
