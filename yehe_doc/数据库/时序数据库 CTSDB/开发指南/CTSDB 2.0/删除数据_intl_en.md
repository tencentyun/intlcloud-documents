#### Request address

The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

#### Request path and method

Request path: `/${metric_name}/_delete_by_query`, where `${metric_name}` is the metric name.
Method: POST

#### Request parameters

None

#### Request content

Query conditions when a metric is deleted. For more information, see the sample.

#### Response content

You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. The error details are in the `error` field.

#### Sample code for curl

Request:

```
curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/ctsdb_test/_delete_by_query -d'
{
"query": {
"bool": {
    "filter": {
        "match_all": {}
        }
    }
}
}'
```

Response:

```
{
"took": 43,
"timed_out": false,
"total": 1,
"deleted": 1,
"batches": 1,
"version_conflicts": 0,
"noops": 0,
"retries": {
    "bulk": 0,
    "search": 0
   }
}
```
