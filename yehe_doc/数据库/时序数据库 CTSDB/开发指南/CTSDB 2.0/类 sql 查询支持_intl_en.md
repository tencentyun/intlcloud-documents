CTSDB 2.0 supports using SQL-like statements for querying, which is only for the convenience of beginners. If you are concerned about the query time, we recommend you use CTSDB's native query statements.

#### Request address

The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

#### Request path and method

Path: `_nlpcn/sql`.
Method: GET

#### Request parameters

You can add the `pretty` parameter value when querying to get the response in a sorted format. For details, see the sample.

#### Request content

Queries mainly include regular queries and aggregate queries. For the specific request content, see the samples.

#### Response content

You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, see the `error` field description. If the parameter or metric name is incorrect, you need to check and correct it on your own.

#### Sample code for curl

For specific queries, see the following samples:

The metric structure used by all samples is as follows:

```
   {
       "ctsdb_test" : {
         "tags" : {
           "region" : "string"
         },
         "time" : {
           "name" : "timestamp",
           "format" : "epoch_millis"
         },
         "fields" : {
           "cpuUsage" : "float",
           "diskUsage" : "string",
           "dcpuUsage" : "integer"
         },
         "options" : {
           "expire_day" : 7,
           "refresh_interval" : "10s",
           "number_of_shards" : 5
         }
       }
   }
```

Sample code of regular query for curl:

```
curl -u root:le201909 -H 'Content-Type: application/json' -XGET 172.16.345.14:9201/_nlpcn/sql?pretty -d 'select docvalue(cpuUsage) from ctsdb_test limit 1'
```

Sample response of regular query:
```
{
  "took" : 22,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 3,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "ctsdb_test@1646064000000_1",
        "_type" : "_doc",
        "_id" : "XMzBRX8BfqojiIOn8jFa",
        "_score" : 1.0,
        "fields" : {
          "cpuUsage" : [
            10.0
          ]
        }
      }
    ]
  }
}
```

> Note:
>
> During regular query, `docvalue` should be added to the field to be queried, so that the instance can get the data from its columnar storage.


Sample code of regular query with search criteria for curl:

```
curl -u root:le201909 -H 'Content-Type: application/json' -XGET 172.16.345.14:9201/_nlpcn/sql?pretty -d 'select docvalue(cpuUsage) from ctsdb_test where region="shanghai" limit 1'
```

Sample response of regular query with search criteria:
```
{
  "took" : 13,
  "timed_out" : false,
  "_shards" : {
    "total" : 10,
    "successful" : 10,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 0.0,
    "hits" : [
      {
        "_index" : "ctsdb_test@1646064000000_1",
        "_type" : "_doc",
        "_id" : "XszBRX8BfqojiIOn8jFb",
        "_score" : 0.0,
        "fields" : {
          "cpuUsage" : [
            30.0
          ]
        }
      }
    ]
  }
}
```

> Note:
>
> For regular queries with search criteria, there is no need to add `docvalue` to the fields used as criteria.



Sample code of aggregate query grouped by tag for curl:

```
curl -u root:le201909 -H 'Content-Type: application/json' -XGET 172.16.345.14:9201/_nlpcn/sql?pretty -d 'select max(cpuUsage) from ctsdb_test group by region'
```

Sample response of aggregate query grouped by tag:
```
{
  "took" : 33,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 3,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "region" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 0,
      "buckets" : [
        {
          "key" : "beijing",
          "doc_count" : 1,
          "MAX(cpuUsage)" : {
            "value" : 20.0
          }
        },
        {
          "key" : "chengdu",
          "doc_count" : 1,
          "MAX(cpuUsage)" : {
            "value" : 10.0
          }
        },
        {
          "key" : "shanghai",
          "doc_count" : 1,
          "MAX(cpuUsage)" : {
            "value" : 30.0
          }
        }
      ]
    }
  }
}
```

> Note:
>
> For aggregate queries grouped by tag, there is no need to add `docvalue` to the field used for grouping.

Sample code of aggregate query grouped by time for curl:

```
curl -u root:le201909 -H 'Content-Type: application/json' -XGET 172.16.345.14:9201/_nlpcn/sql?pretty -d 'select max(cpuUsage) from ctsdb_test GROUP BY date_histogram(field="timestamp","interval"="1d")'
```

Sample response of aggregate query grouped by time:

```
{
  "took" : 30,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 3,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "date_histogram(field=timestamp,interval=1d)" : {
      "buckets" : [
        {
          "key_as_string" : "2022-03-01 00:00:00",
          "key" : 1646092800000,
          "doc_count" : 3,
          "MAX(cpuUsage)" : {
            "value" : 30.0
          }
        }
      ]
    }
  }
}
```


