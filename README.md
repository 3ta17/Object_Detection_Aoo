
# Case Study: Anti-Money Laundering Analysis

## Summary of Work
- **Aggregations and visualizations**: Gained insights from transaction data.
- **Statistics**: Performed detailed analyses to identify anomalies.
- **Data enrichment**: Enhanced data with external sources to increase context.
- **Anti-money laundering**: Identified suspicious activities and flagged them.

## Key Functions and Usage Examples

| **Function**         | **Usage Example**                                                               |
|-----------------------|---------------------------------------------------------------------------------|
| `pd.merge`           | Combined customer information with their transactions.                         |
| `groupby()`          | Aggregated transaction data by customer ID for summary statistics.             |
| `np.where`           | Flagged transactions above a suspicious threshold for further review.          |
| `plt.bar`            | Visualized transaction volumes per customer category.                          |
| `scipy.stats.zscore` | Detected outliers in transaction amounts using z-scores.                       |

## Technologies Used to Achieve Results
- **Python**: Programming and data analysis.
- **Pandas**: Data manipulation and cleaning.
- **Numpy**: Numerical computations.
- **Matplotlib**: Data visualization.
- **Scipy**: Statistical analysis.

---

## Python Code Examples

### 1. Combining Customer and Transaction Data
```python
import pandas as pd

# Example DataFrames
customers = pd.DataFrame({
    'customer_id': [1, 2, 3],
    'name': ['Alice', 'Bob', 'Charlie']
})
transactions = pd.DataFrame({
    'transaction_id': [101, 102, 103],
    'customer_id': [1, 2, 3],
    'amount': [200, 500, 150]
})

# Merge customer and transaction data
merged_data = pd.merge(customers, transactions, on='customer_id')
print(merged_data)
```

### 2. Aggregating Transaction Data
```python
# Aggregating transactions by customer
aggregated_data = merged_data.groupby('customer_id')['amount'].sum()
print(aggregated_data)
```

### 3. Flagging Suspicious Transactions
```python
import numpy as np

# Flagging transactions above a threshold
threshold = 300
merged_data['flagged'] = np.where(merged_data['amount'] > threshold, 'Suspicious', 'Normal')
print(merged_data)
```

### 4. Visualizing Transaction Volumes
```python
import matplotlib.pyplot as plt

# Visualizing transaction volumes per customer
merged_data.groupby('name')['amount'].sum().plot(kind='bar')
plt.xlabel('Customer')
plt.ylabel('Total Transaction Amount')
plt.title('Transaction Volume by Customer')
plt.show()
```

### 5. Detecting Outliers in Transaction Amounts
```python
from scipy.stats import zscore

# Calculating z-scores for transaction amounts
merged_data['zscore'] = zscore(merged_data['amount'])
merged_data['outlier'] = np.where(merged_data['zscore'].abs() > 2, 'Yes', 'No')
print(merged_data)
```
