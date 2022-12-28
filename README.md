
![rob drawio (1)](https://user-images.githubusercontent.com/39345855/209746872-53ecabb6-100d-4900-8beb-cd8545ca8fbe.png)

#### Projecty Summary 
* Coming up exciting hands on project for beginner to try. you are senior data engineer Incharge of building transaction datalake with Apache hudi. we want to bring data with CDC(Change data capture) we will leverage the use of Debezium to bring the data from source and use Schema Register to Register scheme. once we have the Schema Register all changes happening on tables will be broadcasted to Kafka topic and we will use Kafka Connect S3 Sink to bring data into Datalake. We will the process data on Batch Bases Glue job will run on CRON at night will pick up raw files and process them and then perform an UPSERT on datalake.

#### Why HUDI ?

* Apache Hudi (pronounced “hoodie”) is the next generation streaming data lake platform. Apache Hudi brings core warehouse and database functionality directly to a data lake. Hudi provides tables, transactions, efficient upserts/deletes, advanced indexes, streaming ingestion services, data clustering/compaction optimizations, and concurrency all while keeping your data in open source file formats.

* Not only is Apache Hudi great for streaming workloads, but it also allows you to create efficient incremental batch pipelines. Read the docs for more use case descriptions and check out who's using Hudi, to see how some of the largest data lakes in the world including Uber, Amazon, ByteDance, Robinhood and more are transforming their production data lakes with Hudi.
