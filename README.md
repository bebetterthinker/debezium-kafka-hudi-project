
![rob drawio (1)](https://user-images.githubusercontent.com/39345855/209746872-53ecabb6-100d-4900-8beb-cd8545ca8fbe.png)

#### Projecty Summary 
* Coming up exciting hands on project for beginner to try. you are senior data engineer Incharge of building transaction datalake with Apache hudi. we want to bring data with CDC(Change data capture) we will leverage the use of Debezium to bring the data from source and use Schema Register to Register scheme. once we have the Schema Register all changes happening on tables will be broadcasted to Kafka topic and we will use Kafka Connect S3 Sink to bring data into Datalake. We will the process data on Batch Bases Glue job will run on CRON at night will pick up raw files and process them and then perform an UPSERT on datalake.

#### Why HUDI ?

* Apache Hudi (pronounced “hoodie”) is the next generation streaming data lake platform. Apache Hudi brings core warehouse and database functionality directly to a data lake. Hudi provides tables, transactions, efficient upserts/deletes, advanced indexes, streaming ingestion services, data clustering/compaction optimizations, and concurrency all while keeping your data in open source file formats.

* Not only is Apache Hudi great for streaming workloads, but it also allows you to create efficient incremental batch pipelines. Read the docs for more use case descriptions and check out who's using Hudi, to see how some of the largest data lakes in the world including Uber, Amazon, ByteDance, Robinhood and more are transforming their production data lakes with Hudi.

# Steps 

### Step 1:
* CHANGTE THE ACCESS AND SECRET KEY in YML FILE 
```
docker-compose up --build
```

### Step 2: Create Connector Postgres and S3 Sink 
* GO TO http://localhost:3030/kafka-connect-ui/#/cluster/fast-data-dev
![image](https://user-images.githubusercontent.com/39345855/209747515-e9787d72-3449-4162-b026-7dd5b0ea0dac.png)


```
name=PostgresConnector
connector.class=io.debezium.connector.postgresql.PostgresConnector
database.user=postgres
database.dbname=postgres
tasks.max=1
database.hostname=postgres
database.password=postgres
database.server.name=postgres
table.include.list=public.sales
database.port=5432
plugin.name=pgoutput
```


* DO SAME FOR S3 Sinks
 * CHANGE BUCKET NAME 
```
name=s3-sink-connector
connector.class=io.confluent.connect.s3.S3SinkConnector
s3.region=us-east-1
flush.size=1000
schema.compatibility=NONE
topics=postgres.public.sales
tasks.max=1
timezone=UTC
s3.part.size=5242880
locale=PL
format.class=io.confluent.connect.s3.format.json.JsonFormat
storage.class=io.confluent.connect.s3.storage.S3Storage
s3.bucket.name=glue-learn-begineers
rotate.schedule.interval.ms=10000
```

### Step 3: Start Inserting into sales tables 
```
python python-producer-posgres.py

```

### Step 4: Check your S3
![image](https://user-images.githubusercontent.com/39345855/209747806-8e04086f-bb34-45a0-a9b9-d23a3faf4b54.png)


#### Step 5 : Run your Glue Notebooks and Query your processed data 
* https://github.com/soumilshah1995/debezium-kafka-hudi-project/blob/main/hudi%20(1).ipynb

![image](https://user-images.githubusercontent.com/39345855/209749394-9a1fc8f7-6437-43f7-b2b3-44855428a8b9.png)



#### Special Thanks Authors 
* amalioadam
* https://github.com/soumilshah1995/kafka-connect-mysql-s3
