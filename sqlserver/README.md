## ** IN CONSTRUCTION ** 



# GoCdc - A lightweight middleware streaming for change data capture (CDC).

GoCdc is an open source, lightweight __Change Database Capture__ streaming application, connecting changes in a Database to a Kafka streaming.
GoCdc was developed with simplicity in mind, the idea is to have an easy setup with a REST API. 

## Connecting to SqlServer

docker-compose up
access db:

Run:
```bash
docker exec -it eab5ff8034b6  "bash"
/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P P4ssW0rd
```

Check if CDC is enabled -> 
```sql
SELECT [name], database_id, is_cdc_enabled FROM sys.databases;
GO
```

Create a Database:
```sql
CREATE DATABASE TestCdcDb;
GO
```

Enable CDC for the database:
```sql
USE TestCdcDb 
GO 
EXEC sys.sp_cdc_enable_db 
GO 
```

Create a table for testing:
```sql
USE TestCdcDb
GO
CREATE TABLE dummy_table (id INT, name VARCHAR(50))
GO
```


Verify if your table is being tracked by cdc:
```sql
USE TestCdcDb 
GO 
SELECT [name], is_tracked_by_cdc  
FROM sys.tables 
GO  
```

```sql
USE TestCdcDb 
GO 
EXEC sys.sp_cdc_enable_table 
@source_schema = N'dbo', 
@source_name   = N'dummy_table', 
@role_name     = NULL 
GO
```

If you want to disable CDC table :
```sql
USE TestCdcDb 
GO 
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'dbo',   
    @source_name = N'dummy_table',  
    @capture_instance = N'dbo_dummy_table';  
GO
```

Visualize all tables :
```sql
SELECT * FROM databaseName.INFORMATION_SCHEMA.TABLES;
GO
```



READ MORE (Continue tutorial): https://www.red-gate.com/simple-talk/sql/learn-sql-server/introduction-to-change-data-capture-cdc-in-sql-server-2008/








build go app with vendor: go build -mod vendor 


kafka -> https://linuxhint.com/docker_compose_kafka/
https://github.com/abhirockzz/kafka-go-docker-quickstart/blob/master/producer/kafka-producer.go


$ docker exec -it kafka bash
$ ## To create a new topic named test
bash-4.4# kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic test
 
## To start a producer that publishes datastream from standard input to kafka
bash-4.4# kafka-console-producer.sh --broker-list localhost:9092 --topic test