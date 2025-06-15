This project analyzes a Portuguese bank's marketing campaign data collected between May 2008 and November 2010. The dataset does not represent a single marketing campaign, but rather a collection of multiple direct marketing campaigns conducted by a Portuguese bank between the specified period. However, the exact number of campaigns is not explicitly stated. The data captures both:

- Current campaign activity (campaign variable),

- Historical contact efforts (previous, pdays, and poutcome variables).

So while we can infer that multiple campaigns occurred over the 2.5-year period, there is no precise count provided, therefore, these variables indicate that clients may have been contacted multiple times across different campaigns. 

### Ouput Variable

| **Feature** | **Description**                                           |
|-------------|-----------------------------------------------------------|
| `y`         | Has the client subscribed a term deposit? (`yes`/`no`)   |

###  Bank Client Data

| **Feature** | **Description**                                                                 |
|-------------|---------------------------------------------------------------------------------|
| `age`       | Client’s age (numeric)                                                         |
| `job`       | Type of job (e.g. 'admin.', 'blue-collar', 'entrepreneur', etc.)               |
| `marital`   | Marital status: 'divorced', 'married', 'single', 'unknown'                     |
| `education` | Level of education (e.g. 'basic.4y', 'university.degree', 'unknown')            |
| `default`   | Has credit in default? ('yes', 'no', 'unknown')                                 |
| `housing`   | Has a housing loan? ('yes', 'no', 'unknown')                                    |
| `loan`      | Has a personal loan? ('yes', 'no', 'unknown')                                   |

### Last Contact of Current Campaign

| **Feature**     | **Description**                                                                                   |
|-----------------|---------------------------------------------------------------------------------------------------|
| `contact`       | Contact communication type: 'cellular', 'telephone'                                               |
| `month`         | Last contact month: 'jan' to 'dec'                                                                |
| `day_of_week`   | Last contact day of the week: 'mon' to 'fri'                                                      |
| `duration`      | Last contact duration (in seconds). Strongly affects outcome — should be excluded from modeling |

### Campaign History

| **Feature** | **Description**                                                                 |
|-------------|---------------------------------------------------------------------------------|
| `campaign`  | Number of contacts in this campaign (numeric)                                   |
| `pdays`     | Days since client was last contacted in previous campaign (999 = never contacted) |
| `previous`  | Number of contacts before this campaign                                         |
| `poutcome`  | Outcome of previous campaign: 'failure', 'nonexistent', 'success'               |

### Economic Indicators

| **Feature**        | **Description**                                   |
|--------------------|---------------------------------------------------|
| `emp.var.rate`     | Employment variation rate (quarterly)            |
| `cons.price.idx`   | Consumer price index (monthly)                   |
| `cons.conf.idx`    | Consumer confidence index (monthly)              |
| `euribor3m`        | Euribor 3-month rate (daily)                     |
| `nr.employed`      | Number of employees (quarterly)                  |


### Model Comparison: Classification Report Summary

| **Model**           | **Accuracy** | **Class 1 Precision** | **Class 1 Recall** | **Class 1 F1-score** | **Best F1 Score (CV)** | **Training Time (s)** |
|---------------------|--------------|------------------------|--------------------|-----------------------|------------------------|------------------------|
| Logistic Regression | 0.83         | 0.36                   | 0.65               | 0.46                  | 0.45                   | 61.66                  |
| KNN (k=15, p=1)     | 0.90         | 0.64                   | 0.23               | 0.34                  | —                      | 18.63                  |
| SVM (RBF kernel)    | 0.90         | 0.59                   | 0.28               | 0.38                  | 0.35                   | 75.99                  |
| Decision Tree       | 0.90         | 0.66                   | 0.27               | 0.39                  | 0.38                   | 2.71                   |


- Best Recall (Class 1): Logistic Regression (0.65) — A recall of 0.65 means 65% of real subscribers were successfully predicted as subscribers.

- Best F1 Score (Class 1): Logistic Regression (0.46) — more balanced. Logistic Regression has the highest F1, which tells us it’s the most balanced model in catching true subscribers while keeping false alarms in check.

- Fastest Training: Decision Tree (2.71s) — Decision Tree trained super fast — way quicker than Logistic (60s) or SVM (76s).

- Consistent Accuracy Across Models: KNN, Decision Tree, and SVM all at ~90%.


### Model Selection Guide Based on Business Goals

| **Scenario**                          | **Recommended Model**     | **Why**                                                                 |
|--------------------------------------|----------------------------|--------------------------------------------------------------------------|
| Maximize campaign reach              | Logistic Regression        | High recall ensures more real "Yes" responders are found                |
| Prioritize precision (conservative)  | Decision Tree / SVM        | Fewer false positives if budget/call center capacity is limited          |
| Prioritize speed & interpretability  | Decision Tree              | Fast training + easy to explain to business stakeholders                 |
| Highest raw accuracy (with caution)  | KNN                        | Great overall accuracy but poor detection of converters (low recall)     |


## Best Overall Model: Logistic Regression

| **Metric**       | **Value**             | **Meaning**                                                                                      |
|------------------|------------------------|--------------------------------------------------------------------------------------------------|
| **Accuracy**     | 0.83                   | Model correctly predicted 83% of total cases but important to note imbalance bias.                    |
| **Macro Avg**    | 0.66 / 0.75 / 0.68     | Equal weight to both classes — reveals that performance is stronger on majority class (Class 0). |
| **Weighted Avg** | 0.88 / 0.83 / 0.85     | Accounts for class imbalance — heavily influenced by dominant Class 0 due to its higher support. |

### Confusion Matrix – Logistic Regression

|                        | **Predicted No (0)**         | **Predicted Yes (1)**         |
|------------------------|------------------------------|-------------------------------|
| **Actual No (0)**      | 9378 (True Negatives)      | 1587 (False Positives)      |
| **Actual Yes (1)**     | 492 (False Negatives)      | 900 (True Positives)        |

### Key Insights

- High recall: 65% of real subscribers were identified correctly.

- The Logistic Regression model is conservative in predicting "Yes" — better at identifying definite "No"s.

- But it still captures 900 true positives, which is ~65% of actual converters — that’s great for marketing.

- False positives could lead to wasted marketing resources. The 1587 false positives (predicting someone will convert, but they won’t) may waste marketing resources.

  
### Top Positive Influencers (Features that Increase Probability of Subscription)

| **Feature**              | **Insight**                                                                                     |
|--------------------------|--------------------------------------------------------------------------------------------------|
| `euribor3m`              | When interest rates (3-month Euribor) are higher, people may be more interested in term deposits. |
| `nr.employed`            | Higher employment levels may increase confidence and subscription rates.                         |
| `job_retired`            | Retired clients seem more likely to subscribe (possibly due to stable income and savings goals).  |
| `education_basic.6y`     | Customers with basic education might view term deposits as a safer investment.                   |
| `loan_yes`               | Those with existing loans may be more open to saving plans like term deposits.                   |


### Top Negative Influencers (Features that Reduce Probability of Subscription)

| **Feature**                             | **Insight**                                                                                      |
|----------------------------------------|--------------------------------------------------------------------------------------------------|
| `contact_telephone`                    | Customers contacted via telephone (vs. cellular) were much less likely to subscribe.            |
| `month_may`                            | Campaigns in May had lower success rates — possibly due to timing or seasonality.              |
| `campaign`                             | More contact attempts within the same campaign correlate with lower success (over-contact fatigue?). |
| `job_blue-collar`, `job_housemaid`, `job_services` | Customers in certain job types were less likely to subscribe.                      |
| `day_of_week_mon`, `day_of_week_tue`  | Calling on Monday or Tuesday may yield poorer results compared to other days.                  |
| `previous`                             | More contacts in previous campaigns might lead to fatigue or indicate prior disinterest.       |
