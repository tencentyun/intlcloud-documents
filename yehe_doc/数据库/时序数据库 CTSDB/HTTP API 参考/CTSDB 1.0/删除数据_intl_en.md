
## Request Address 
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

## Request Path and Method
Request path: `/${metric_name}/_delete_by_query`, where `${metric_name}` is the metric name.
Method: POST

## Request Parameters 
None

## Request Content
Query conditions when a metric is deleted. For more information, please see the sample.

## Response Content
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. The specific error information is in the `error` field. Note: if the request succeeded but the `errors` (not `error`) field is not `false`, the specific data that failed to be written is indicated in the `errors` field.

## Sample Code for curl 
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
