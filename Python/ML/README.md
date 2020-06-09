# Python ML

## scikit-learn

### Cross-validation

```python
rfecv = RFECV(estimator=rf, step=1, cv=SratifiedKFold(2), scoring='roc_auc')
rfecv.fit(X_rain, y_train)

print(f'Optimal number of features: {rfecv.n_features_}')

plt.figure()
plt.xlabel('Number of features selected')
plt.ylabel('Cross validation score')
plt.plot(range(1, len(rfecv.grid_scores_)+1), rfecv.grid_scores_)
plt.show()
```
