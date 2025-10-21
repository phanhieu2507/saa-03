# Athena
- serverless
- uses SQL Language
- interactive query service to analyse data in s3
- per only per queries run
- process logs
- ad hoc analysis
- expensive if data is not columnar
- store results back to [[S3]]

## Use
- commonly used with quicksight
- buisness intel, alaytics, reporting
- use glue to covert data to parquet or orc
- partition data by path
```
pathtoBucket/pathtotable
                        /partition_col_key
                        /partionen_col_key
```
- use larger files

## Supported Data types
- CSV
- JSON
- ORC
- Avro
- Parquet (faster than csv)

## Price
- 5 Dollar per TB scanned

## Federated query
- query data from outside from [[S3]] (relational db, non relation db, onpremise...)
- use data source connectior ([[Lambda]] function which connects to another service)

![[Screenshot 2025-10-13 at 10.48.24.png]]

the table of athena doesn't contain the data, it contain the information on how to convert the source data to be able to query on it
 output can be on the console saved or output to other aws tools
 ![[Screenshot 2025-10-13 at 10.59.53.png]]
 dont need to think about the loading and tranformation 
 ![[Screenshot 2025-10-13 at 11.02.44.png]]