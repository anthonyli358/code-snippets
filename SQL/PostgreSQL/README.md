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

### Cast to mon, yyyy

```sql
to_char(date_trunc('month', created_at)::date,'MON, YYYY') AS month
```

### Cast to week

```sql
date_trunc('week', created_at::date) as week
```

### Median (intepolate)

```sql
percentile_cont(0.5) within group(order by heights) as median_height
```

### Generate series of dates

```sql
generate_series('2019-12-01', now(), '1 day'::interval) as day
```

### Generate custom values

```sql
(select *
from (values
    ('guitar', 'string'),
    ('trumpet', 'brass'),
    ('flute', 'woodwind'),
) AS t (instrument, type)
```
