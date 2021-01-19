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

## PostgreSQL

### AWS DB

```python
from sshtunnel import SSHTunnelForwarder  # run pip install sshtunnel
from sqlalchemy.orm import sessionmaker
from sqlalchemy import create_engine
import paramiko
import psycopg2  # run pip install psycopg2-binary

import pandas as pd
import json

pkey = paramiko.RSAKey.from_private_key_file('<pkey_path>', password='<pkey_password>'])  # optional

with SSHTunnelForwarder(
    ('<server>', 22),  # remote server IP and SSH port
    ssh_username='<username>',
    ssh_pkey='<pkey_path>',  # or pkey if using paramiko line above
    ssh_private_key_password='<pkey_password>',  # not needed if using paramiko line above
    remote_bind_address=('<host/socket>', 5432)) as server:  # PostgreSQL server IP and server port on remote machine
        
        server.start()  # start ssh sever
        print('Server connected via SSH')

        # connect to PostgreSQL
        local_port = str(server.local_bind_port)
        engine = create_engine('postgresql://<username>:<password>@127.0.0.1:' + local_port +'/<database_name>')
        Session = sessionmaker(bind=engine)
        session = Session()
        print('Database session created')

        # test data retrieval
        result = session.execute("""
            SELECT * 
            FROM <database_table>
            LIMIT 10
            """)

        session.close()
        
df = pd.DataFrame(result.fetchall(), columns=result.keys())
print(df)
```