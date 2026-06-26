# Message Intelligence System

---

## Objective

The goal of this project is to build a classification system that identifies whether incoming digital messages are **Spam** or **Legitimate**. Three different machine learning algorithms are combined and compared — KNN, SVM, and Naive Bayes — to analyze how different assumptions impact model performance.

---

## Problem Statement

A communication security company wants to automatically classify user messages as:

- `0` → Legitimate Message
- `1` → Spam Message

The dataset contains message-related features extracted from text (numerical summaries) and user behavior signals. The task is to build and compare multiple classification models and explain their performance using probability concepts.

---

## Dataset Description

**File:** `Message_Intelligence_Dataset_5200.csv`  
**Total Records:** 5,200 messages  
**Target Variable:** `spam_label` (0 = Legitimate, 1 = Spam)

| Column | Description |
|---|---|
| message_id | Unique identifier for each message |
| message_text | Raw message content |
| message_length | Total character length of the message |
| word_count | Number of words in the message |
| num_urls | Number of URLs present in the message |
| num_digits | Count of digit characters |
| num_special_chars | Count of special characters |
| spam_keyword_score | Score based on spam-related keywords |
| legit_keyword_score | Score based on legitimate keywords |
| sender_activity_score | Activity score of the sender |
| sender_account_age_days | Age of sender account in days |
| messages_sent_last_24h | Number of messages sent by sender in last 24 hours |
| timestamp | Date and time the message was sent |
| hour_of_day | Hour when the message was sent (0–23) |
| day_of_week | Day of the week (0=Monday, 6=Sunday) |
| spam_label | Target variable (0=Legitimate, 1=Spam) |

**Class Distribution:**
- Legitimate (0): 4,227 messages (81.3%)
- Spam (1): 973 messages (18.7%)

---

## Libraries Used

```python
pandas
numpy
matplotlib
seaborn
scikit-learn
warnings
```
---

## Project Parts Covered

### Part A — Theory
- Conditional Probability
- Bayes' Theorem
- Naive Bayes assumptions
- KNN and SVM working principles
- Comparison of distance-based, probabilistic, and margin-based classifiers

### Part B — Dataset Understanding & Preparation
- Identified input features and target variable
- Handled missing values (median imputation)
- Applied StandardScaler for feature scaling
- Split data: 80% training / 20% testing (stratified)

### Part C — K-Nearest Neighbors (KNN)
- Tested K values: 1, 3, 5, 7, 9, 11, 15, 21
- Compared Euclidean vs Manhattan distance metrics
- Identified misclassified messages (False Positives and False Negatives)
- Best K selected based on F1 Score

### Part D — Support Vector Machine (SVM)
- Trained with Linear kernel
- Trained with RBF kernel
- Analyzed support vectors and margin separation
- Compared SVM vs KNN performance

### Part E — Naive Bayes Classifier
- Implemented GaussianNB classifier
- Manually computed conditional probabilities using Bayes' Theorem
- Compared theoretical calculation with model predictions

### Part F — Model Comparison & Evaluation
- Metrics used: Accuracy, Precision, Recall, F1 Score
- ROC Curves with AUC values plotted for all models
- Identified best model for high precision and high recall

### Part G — Final Analysis & Report
- Strengths and weaknesses of each classifier
- Impact of probability assumptions in Naive Bayes
- Trade-offs between interpretability and performance
- Business recommendation for real-world deployment

---

## Model Results Summary

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| KNN (K=7) | 99.90% | 99.74% | 99.74% | 99.74% |
| SVM (Linear) | 100.00% | 100.00% | 100.00% | 100.00% |
| SVM (RBF) | 100.00% | 100.00% | 100.00% | 100.00% |
| Naive Bayes | 100.00% | 100.00% | 100.00% | 100.00% |

**Best Model:** SVM (RBF Kernel) — recommended for production deployment  
**Most Interpretable:** Naive Bayes — recommended for audit and compliance

---

## Key Findings

- `spam_keyword_score`, `num_urls`, and `legit_keyword_score` are the strongest predictors of spam.
- The dataset features are well-separated, allowing all models to achieve very high accuracy.
- Manual Bayes' Theorem calculation confirmed: a message with a URL has a significantly higher probability of being spam.
- For real-world deployment, **high Recall is more important** than Precision in spam detection — it is more harmful to let spam through than to occasionally flag a legitimate message.

---

## Business Recommendation

**Primary Model:** SVM (RBF Kernel) — best accuracy and recall for production use.  
**Secondary Model:** Naive Bayes — for explainability and audit trail.  
**Deployment pipeline:** Incoming message → Feature Extraction → Scaling → SVM (RBF) → Prediction.  
For edge cases (uncertain predictions), route to Naive Bayes for a second probability-based opinion.

---

