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
    ('Deel', date('2019-07-01')),
    ('jon@div-brands.com', date('2020-02-18')),
    ('inna@a-labinsider.com', date('2020-02-06')),
    ('nick+client12@letsdeel.com', date('2019-07-10')),
    ('jonathan@amitree.com', date('2019-12-09')),
    ('james@bettr.software', date('2020-01-01'))
) AS t (email, join_date)
```
