This document describes how to consume Kafka data in real time by using the Apache Druid Kafka indexing service. Before performing operations described in this document, just like in a Hadoop cluster, you need to make sure that the Kafka and Druid clusters can properly communicate with each other.

>?
>- The two clusters should be in the same VPC. If they are in different VPCs, the two VPCs should be able to communicate with each other (through CCN or Peering Connection, for example).
>- If necessary, you should configure the Druid cluster with the host information of the Kafka cluster.

## Using Command Line

1. Start the Kafka broker in the Kafka cluster.
```
./bin/kafka-server-start.sh config/server.properties
```
1. Create a Kafka topic named `mytopic`.
```
./bin/kafka-topics.sh --create --zookeeper {kafka_zk_ip}:2181 --replication-factor 1 --partitions 1 --topic mytopic
Output:
Created topic "mytopic".
```
`{kafka_zk_ip}:2181` is the ZooKeeper address of the Kafka cluster.
1. Prepare a data description file `kafka-mytopic.json` in the Druid cluster.
```
{
     "type": "kafka",
     "dataSchema": {
         "dataSource": "mytopic-kafka",
         "parser": {
             "type": "string",
             "parseSpec": {
                 "timestampSpec": {
                     "column": "time",
                     "format": "auto"
                 },
                 "dimensionsSpec": {
                     "dimensions": ["url", "user"]
                 },
                 "format": "json"
             }
         },
         "granularitySpec": {
             "type": "uniform",
             "segmentGranularity": "hour",
             "queryGranularity": "none"
         },
         "metricsSpec": [{
                 "type": "count",
                 "name": "views"
             },
             {
                 "name": "latencyMs",
                 "type": "doubleSum",
                 "fieldName": "latencyMs"
             }
         ]
     },
     "ioConfig": {
         "topic": "mytopic",
         "consumerProperties": {
             "bootstrap.servers": "{kafka_ip}:9092",
             "group.id": "kafka-indexing-service"
         },
         "taskCount": 1,
         "replicas": 1,
         "taskDuration": "PT1H"
     },
     "tuningConfig": {
         "type": "kafka",
         "maxRowsInMemory": "100000"
     }
 }
```
`{kafka_ip}:9092` is the IP and port of the `bootstrap.servers` in your Kafka cluster.
1. Add the Kafka supervisor on the master nodes in the Druid cluster.
```
curl -XPOST -H 'Content-Type: application/json' -d @kafka-mytopic.json http://{druid_master_ip}:8090/druid/indexer/v1/supervisor
Output:
{"id":"mytopic-kafka"}
```
`{druid_master_ip}:8090` is the node where the `overload` process is deployed, which is generally a master node.
1. Enable a console producer in the Kafka cluster.
```
./bin/kafka-console-producer.sh --broker-list {kafka_ip}:9092 --topic mytopic
```
`{kafka_ip}:9092` is the IP and port of the `bootstrap.servers` in your Kafka cluster.
1. Prepare a query file named `query-mytopic.json` in the Druid cluster.
```
{
     "queryType" : "search",
     "dataSource" : "mytopic-kafka",
     "intervals" : ["2020-03-13T00:00:00.000/2020-03-20T00:00:00.000"],
     "granularity" : "all",
     "searchDimensions": [
         "url",
         "user"
     ],
     "query": {
         "type": "insensitive_contains",
         "value": "roni"
     }
 }
```
1. Enter some data on Kafka in real time.
```
{"time": "2020-03-19T09:57:58Z", "url": "/foo/bar", "user": "brozo", "latencyMs": 62}
{"time": "2020-03-19T16:57:59Z", "url": "/", "user": "roni", "latencyMs": 15}
{"time": "2020-03-19T17:50:00Z", "url": "/foo/bar", "user": "roni", "latencyMs": 25}
```
Timestamp generation command:
```
python -c 'import datetime; print(datetime.datetime.utcnow().strftime("%Y-%m-%dT%H:%M:%SZ"))'
```
1. Perform a query in the Druid cluster.
```
curl -XPOST -H 'Content-Type: application/json' -d @query-mytopic.json http://{druid_ip}:8082/druid/v2/?pretty
```
`{druid_ip}:8082` is the broker node of your Druid cluster, which generally resides on a master or router node.
**Query result:**
```
[ {
  "timestamp" : "2020-03-19T16:00:00.000Z",
  "result" : [ {
    "dimension" : "user",
    "value" : "roni",
    "count" : 2
  } ]
} ]
```

## Using Web-Based Visualization

You can ingest data from a Kafka cluster and perform queries in the Druid Web UI Console in a visualized manner. For detailed directions, please see [Loading data with the data loader](https://druid.apache.org/docs/latest/tutorials/tutorial-kafka.html#loading-data-with-the-data-loader).
