# R Database Connections

## RMySQL

### RMySQL connection

```r
db_query <- function(query_syntax, number_rows_parameter=-1, return_indicator=1){
	on.exit(dbDisconnect(connection))
	connection <- dbConnect(MySQL(), user='', password='', host ='')
	
	query <- dbSendQuery(connection, query_syntax)
	data = fetch(query, n=number_rows_parameter)
	if (return_indicator=-1){
		return(data)
	}
}
```

### Kill connections

```r
killDBConnections <- function(){
	all_cons <- dbListConnections(MySQL())
	print(all_cons)
	for(con in all_cons)
		+ dbDisconnect(con)
	print(paste(length(all_cons), " connections killed."))
}
```

## RODBC

### RODBC connection

```r
db_query <- function(query_syntax){
	odbc_connection <- odbcConnection('dwodbc')
	sqlQuery(odbc_connection, query_syntax)
}
```

### Snowflake ODBC connection

```r
sf_query <- function(query_syntax){
	odbc_connection <- odbcConnect('snowflake_odbc', uid='', pwd='')
	sqlQuery(odbc_connection, query_syntax)
}
```

