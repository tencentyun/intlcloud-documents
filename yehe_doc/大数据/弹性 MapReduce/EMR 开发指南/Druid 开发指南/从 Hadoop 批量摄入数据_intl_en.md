This document describes how to load data files from a remote Hadoop cluster into a Druid cluster in batches. Operations in this document are all performed by the `Hadoop` user; therefore, please switch to the `Hadoop` user in both the Druid and Hadoop clusters.

## Loading Data into Druid Cluster in Batches

1. Run the following commands to create directories as the `Hadoop` user in the remote Hadoop cluster:
```
hdfs dfs -mkdir /druid
hdfs dfs -mkdir /druid/segments
hdfs dfs -mkdir /quickstart
hdfs dfs -chmod 777 /druid
hdfs dfs -chmod 777 /druid/segments
hdfs dfs -chmod 777 /quickstart
```
>!If the Druid and Hadoop clusters are both self-deployed clusters, the directories need to be created on the corresponding Hadoop cluster (you also need to perform subsequent operations in the correct cluster). If the Druid and Hadoop clusters are the same cluster in the testing environment, you can perform the operations in the same cluster.
2. Upload the testing package.
The Druid cluster comes with a sample dataset named `Wikiticker` (located in `/usr/local/service/druid/quickstart/tutorial/wikiticker-2015-09-12-sampled.json.gz` by default). The operation of uploading the dataset in the Druid cluster to the corresponding remote Hadoop cluster **should be performed on the remote Hadoop cluster.**
```
hdfs dfs -put wikiticker-2015-09-12-sampled.json.gz /quickstart/wikiticker-2015-09-12-sampled.json.gz
```
3. Compile the index file.
Prepare an index file by running the following commands, which is still the Druid cluster's sample file `/usr/local/service/druid/quickstart/tutorial/wikipedia-index-hadoop.json`:
```
{
  "type" : "index_hadoop",
  "spec" : {
    "dataSchema" : {
      "dataSource" : "wikipedia",
      "parser" : {
        "type" : "hadoopyString",
        "parseSpec" : {
          "format" : "json",
          "dimensionsSpec" : {
            "dimensions" : [
              "channel",
              "cityName",
              "comment",
              "countryIsoCode",
              "countryName",
              "isAnonymous",
              "isMinor",
              "isNew",
              "isRobot",
              "isUnpatrolled",
              "metroCode",
              "namespace",
              "page",
              "regionIsoCode",
              "regionName",
              "user",
              { "name": "added", "type": "long" },
              { "name": "deleted", "type": "long" },
              { "name": "delta", "type": "long" }
            ]
          },
            "column" : "time"
      },
      "metricsSpec" : [],
      "granularitySpec" : {
        "type" : "uniform",
        "segmentGranularity" : "day",
        "rollup" : false
      }
    },
    "ioConfig" : {
      "type" : "hadoop",
      "inputSpec" : {
        "type" : "static",
        "paths" : "/quickstart/wikiticker-2015-09-12-sampled.json.gz"
      }
    },
    "tuningConfig" : {
      "type" : "hadoop",
      "partitionsSpec" : {
        "type" : "hashed",
        "targetPartitionSize" : 5000000
      },
      "forceExtendableShardSpecs" : true,
      "jobProperties" : {
        "yarn.nodemanager.vmem-check-enabled" : "false",
        "mapreduce.map.java.opts" : "-Duser.timezone=UTC -Dfile.encoding=UTF-8",
        "mapreduce.job.user.classpath.first" : "true",
        "mapreduce.reduce.java.opts" : "-Duser.timezone=UTC -Dfile.encoding=UTF-8",
        "mapreduce.map.memory.mb" : 1024,
        "mapreduce.reduce.memory.mb" : 1024
      }
    }
  },
  "hadoopDependencyCoordinates": ["org.apache.hadoop:hadoop-client:2.8.5"]
}
```
**Note:**
 - `hadoopDependencyCoordinates` is the dependent Hadoop version.
 - `spec.ioConfig.inputSpec.paths` is the input file path. If you have already set cluster connectivity in the `common.runtime.properties` configuration item, you can use the relative path (for more information, please see [Druid Usage](https://intl.cloud.tencent.com/document/product/1026/35874)); otherwise, you need to use a relative path starting with `hdfs://` or `cosn://` based on the actual conditions.
 - The `tuningConfig.jobProperties` parameter is used to set MapReduce job parameters.
4. Submit the indexing task.
Submit the task in the Druid cluster to ingest the data. Run the following command as the `Hadoop` user under the Druid directory:
```
./bin/post-index-task --file quickstart/tutorial/wikipedia-index-hadoop.json --url http://localhost:8090
```
If the command succeeds, an output similar to the one below will be displayed:
```
...
Task finished with status: SUCCESS
Completed indexing data for wikipedia. Now loading indexed data onto the cluster...
wikipedia loading complete! You may now query your data
```

## Data Query
Druid supports SQL-like and native JSON queries as described below. For more information, please see [Tutorial: Querying data](https://druid.apache.org/docs/latest/tutorials/tutorial-query.html).

### Querying with SQL
Druid supports multiple SQL query methods:
- Perform queries in the `Query` menu on the web UI.
```
SELECT page, COUNT(*) AS Edits
FROM wikipedia
WHERE TIMESTAMP '2015-09-12 00:00:00' <= "__time" AND "__time" < TIMESTAMP '2015-09-13 00:00:00'
GROUP BY page
ORDER BY Edits DESC
LIMIT 10
```
- Use the command line tool `bin/dsql` for interactive queries on a query node.
```
[hadoop@172 druid]$ ./bin/dsql
Welcome to dsql, the command-line client for Druid SQL.
Connected to [http://localhost:8082/].
Type "\h" for help.
dsql> SELECT page, COUNT(*) AS Edits FROM wikipedia WHERE "__time" BETWEEN TIMESTAMP '2015-09-12 00:00:00' AND TIMESTAMP '2015-09-13 00:00:00' GROUP BY page ORDER BY Edits DESC LIMIT 10;
┌──────────────────────────────────────────────────────────┬───────┐
│ page                                                     │ Edits │
├──────────────────────────────────────────────────────────┼───────┤
│ Wikipedia:Vandalismusmeldung                             │    33 │
│ User:Cyde/List of candidates for speedy deletion/Subpage │    28 │
│ Jeremy Corbyn                                            │    27 │
│ Wikipedia:Administrators' noticeboard/Incidents          │    21 │
│ Flavia Pennetta                                          │    20 │
│ Total Drama Presents: The Ridonculous Race               │    18 │
│ User talk:Dudeperson176123                               │    18 │
│ Wikipédia:Le Bistro/12 septembre 2015                    │    18 │
│ Wikipedia:In the news/Candidates                         │    17 │
│ Wikipedia:Requests for page protection                   │    17 │
└──────────────────────────────────────────────────────────┴───────┘
Retrieved 10 rows in 0.06s.
```
- Submit SQL queries over HTTP.
```
curl -X 'POST' -H 'Content-Type:application/json' -d @quickstart/tutorial/wikipedia-top-pages-sql.json http://localhost:18888/druid/v2/sql
```
The formatted output is as follows:
```
[
    {
        "page":"Wikipedia:Vandalismusmeldung",
        "Edits":33
    },
    {
        "page":"User:Cyde/List of candidates for speedy deletion/Subpage",
        "Edits":28
    },
    {
        "page":"Jeremy Corbyn",
        "Edits":27
    },
    {
        "page":"Wikipedia:Administrators' noticeboard/Incidents",
        "Edits":21
    },
    {
        "page":"Flavia Pennetta",
        "Edits":20
    },
    {
        "page":"Total Drama Presents: The Ridonculous Race",
        "Edits":18
    },
    {
        "page":"User talk:Dudeperson176123",
        "Edits":18
    },
    {
        "page":"Wikipédia:Le Bistro/12 septembre 2015",
        "Edits":18
    },
    {
        "page":"Wikipedia:In the news/Candidates",
        "Edits":17
    },
    {
        "page":"Wikipedia:Requests for page protection",
        "Edits":17
    }
]
```

### Querying through native JSON

- Directly enter JSON queries in the `Query` menu on the web UI.
```
{
     "queryType" : "topN",
     "dataSource" : "wikipedia",
     "intervals" : ["2015-09-12/2015-09-13"],
     "granularity" : "all",
     "dimension" : "page",
     "metric" : "count",
     "threshold" : 10,
     "aggregations" : [
         {
            "type" : "count",
            "name" : "count"
         }
     ]
}
```
- Submit the queries over HTTP under the Druid directory on a query node.
```
curl -X 'POST' -H 'Content-Type:application/json' -d @quickstart/tutorial/wikipedia-top-pages.json http://localhost:18888/druid/v2?pretty
```
The output is as follows:
```
[ {
  "timestamp" : "2015-09-12T00:46:58.771Z",
  "result" : [ {
    "count" : 33,
    "page" : "Wikipedia:Vandalismusmeldung"
  }, {
    "count" : 28,
    "page" : "User:Cyde/List of candidates for speedy deletion/Subpage"
  }, {
    "count" : 27,
    "page" : "Jeremy Corbyn"
  }, {
    "count" : 21,
    "page" : "Wikipedia:Administrators' noticeboard/Incidents"
  }, {
    "count" : 20,
    "page" : "Flavia Pennetta"
  }, {
    "count" : 18,
    "page" : "Total Drama Presents: The Ridonculous Race"
  }, {
    "count" : 18,
    "page" : "User talk:Dudeperson176123"
  }, {
    "count" : 18,
    "page" : "Wikipédia:Le Bistro/12 septembre 2015"
  }, {
    "count" : 17,
    "page" : "Wikipedia:In the news/Candidates"
  }, {
    "count" : 17,
    "page" : "Wikipedia:Requests for page protection"
  } ]
} ]
```
