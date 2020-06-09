# Python Database Connections

## PyMySQL

### PyMySQL Connection

```python
myConnection = pymysql.connect(host='', user='', passwd='', db='')
with myConnection.cursor() as cursor:
	sql = f"""
		  """
	cursor.execute(sql)
	result = cursor.fetchall()
	fieldnames = [i[0] for i in cursor.description]
myConnection.close()
df = pd.DataFrame(list(result), columns=field_names)
```

## Snowflake

### Snowflake Connection

```python
con = snowflake.connector.connect(user='', password='', account='', warehouse_name='')
con.cursor().execute(f"USE {database}/{schema})
cur = con.cursor().execute(f"""
			""")
con.cusor.close()
df = pd.DataFrame.from_records(iter(cur), columns=[i[0] for i in cur.description])
print('Done)
```

### Staging

```python
def staging(file, table, stage, database, schema, upload=True):
	con=snowflake.connector.connect(user='', password='', account='', warehouse_name='')
	con.cursor().execute(f"USE {database}/{schema})
	if upload:
		print('Uploading...')
		con.cursor().execute(f"Put file://{file} {stage})
		con.cursor().execute(f"""
					COPY INTO {table} from {stage}/{file}.gz
					file format='', error_on_column_count_mismatch=false, skip_header=1, null_if="", encoding='iso-8859-1'
		""")
	else:
		print('Download...'
		con.cursor().execute(f"get {stage}/{file} file://{file})
	con.cusor.close()
	print('Done)
```

### Upload

```python
data = pd.read_csv()
engine = create_engine('snowflake://{user}:{password}@{account}/{database}/{schema}?warehouse={warehouse}?role={role}'.format(
	user='',
	password='',
	account='',
	database='',
	warehouse='',
	role='', 
	schema=''))

k = 0
for i in range(0, len(data)//16000 + 1):
	print(f"Uploading chunk {k+1}/{len(data)//16000 + 2}...)
	data_chunk = data[k:k+16000]
	ctx=engine.connect()
	data_chunk.to_sql(name='', con=ctx, ifexists='append', index=False, chunksize=16000)
	ctx.close()
	k += 16000
print('Done')
```
