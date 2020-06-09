# Pandas

### Merge

```python
df = pd.merge(df, df2, how='left', on='key')
```

### Aggregate

```python
df.groupby(['key1', key2']).agg(newvar = pd.NamedAgg(column = 'newvar', aggfunc='count'),
								newvar2 = pd.NamedAgg(column = 'newvar2', aggfunc=lambda x: x.sum() / x.count()).reset_index()
```

### Manipulate cells 

```python
df.loc[(df['key'].isin(list)) & (df.['key2']==0)] = 1
```
