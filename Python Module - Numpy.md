

```python
# Convert pandas Dataframe to Numpy and calculate
def negativeSharpeRatio(weights, returns, covariance, rate):
      portfolio_return = np.dot(weights, returns)
      portfolio_std = np.sqrt(np.dot(weights.T, np.dot(covariance, weights)))
      sharpe_ratio = (portfolio_return - rate) / portfolio_std
      return -sharpe_ratio
```
