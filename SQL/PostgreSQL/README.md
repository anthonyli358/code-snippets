# PostgreSQL

### Extract json with columns

```sql
rates->'rates'->>amount::float
rates->'rates'->>currency::varchar
```

### Cast to yyyy-mm-01

```sql
to_date(cast(created_at as TEXT), 'YYYY-MM-01') as year_mon,
```

### Median (intepolate)

```sql
percentile_cont(0.5) within group(order by heights) as median_height
```
