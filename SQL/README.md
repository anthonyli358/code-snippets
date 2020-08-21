# SQL

### Alias tables

```sql
select 
a.*,
b.column_2
from table_1 a
left join table_2 b on a.column_1 = b.column_1
```

### Temp tables

```sql
with temp_1 as (
    select * from table_1
),

temp_2 as (
    select * from temp_1
)

select * from temp_2
```

### Union tables (same columns, keep duplicates)

```sql
select * from table_1
union all select * from table_2
-- 'union' to remove duplicates
```

### Filtered summary operations

```sql
sum(case when column = 'true' then 1 else 0 end) as total
```
