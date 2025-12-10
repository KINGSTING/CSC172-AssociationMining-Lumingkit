# CSC17 Associate Rule Mining Project Proposal
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/10/25

## 1. Project Title 
Network Intrusion Pattern Discovery

## 2. Problem Statement
<div style="text-align: justify">
This project applies Association Rule Mining (ARM) to network security logs to discover hidden correlations between network traffic features and malicious activity. Unlike standard "Market Basket Analysis" which predicts consumer purchases, this project views a network connection as a "transaction" and its attributes (protocol, service, flag) as "items." The goal is to automatically generate signature-based detection rules for network intrusions.
</div>

## 3. Objectives
<div style="text-align: justify"> 
The primary goal is to identify strong association rules that characterize malicious network traffic. The specific objectives are:

1. **Data Transformation:** To preprocess the NSL-KDD dataset by discretizing continuous network features (e.g., duration, source bytes) and applying One-Hot Encoding to create a transactional format suitable for ARM.

2. **Pattern Extraction:** To implement the Apriori algorithm to extract frequent itemsets relating to specific attack types (e.g., DoS, Probe, R2L).

3. **Rule Evaluation:** To evaluate the discovered rules using standard metrics (Lift, Confidence, Conviction) to differentiate between coincidentally frequent traffic and statistically significant attack signatures.
</div>

## 4. Dataset Plan
- **Source:** ![NSL-KDD Dataset](https://www.kaggle.com/datasets/hassan06/nslkdd) (An improved version of the KDD'99 benchmark).
- **Structure:**
    - **Transactions:** Network connection sessions.
    - **Volume:** ~125,973 records (Training Set), exceeding the 500-record requirement.
    - **Key Attributes:**
        - *protocol_type* (TCP, UDP, ICMP)
        - *service* (HTTP, SMTP, FTP, etc.)
        - *flag* (Connection status like SF, S0, REJ)
        - *class* (Normal vs. Anomaly)
- **Selection:** I will utilize the KDDTrain+_20Percent.txt subset to ensure efficient processing while maintaining statistical significance.

## 5. Technical Approach
- **Algorithm:** Apriori Algorithm (chosen for its interpretability in rule generation).
- **Preprocessing Pipeline:**
    - **Discretization:** Continuous variables will be binned into categorical ranges (e.g., duration $\rightarrow$ short, medium, long).
    - **Encoding:** TransactionEncoder will be used to convert categorical data into a boolean (One-Hot) matrix.
- **Tools & Libraries:**
    - **Language:** *Python*
    - **Libraries:** [![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://python.org) [![Pandas](https://img.shields.io/badge/Pandas-Data_Manipulation-150458)](https://pandas.pydata.org) [![mlxtend](https://img.shields.io/badge/mlxtend-Association_Mining-orange)](http://rasbt.github.io/mlxtend/) [![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-9cf)](https://seaborn.pydata.org)
- **Environment:** Jupyter Notebook / Google Colab.

## 6. Expected Challenges & Mitigations

**Challenge 1:** Handling Continuous Data (ARM requires categorical data, but network logs have numbers)
> **Solution 1:** Apply statistical binning (e.g., using pandas.cut) to convert numerical columns like src_bytes and duration into categorical bins (e.g., "High-Traffic", "Zero-Duration") before encoding.

**Challenge 2:** Rule Explosion (Generating thousands of redundant or obvious rules).
> **Solution 2:** Strict hyperparameter tuning. I will set a higher min_support threshold (e.g., 0.05) to filter out noise and use the Lift metric to prune rules that are statistically independent (Lift $\approx$ 1).
