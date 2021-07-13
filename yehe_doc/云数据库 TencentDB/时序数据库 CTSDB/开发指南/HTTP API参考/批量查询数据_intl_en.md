
## Request Address 
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

## Request Path and Method
Path: `/_msearch`
Method: GET

## Request Parameters 
You can set the `_routing` parameter during data write to improve the query efficiency as instructed in the sample. You can also set the `filter_path` parameter to filter and simplify the returned results. Its value contains multiple JSON paths separated by commas, and each JSON path is constructed by concatenating elements with dots. You can also use the `\*` wildcard to match any character, the `\*\*` wildcard to match any path, and the `-` prefix to remove certain returned fields.
For example, `responses._shards.f\*` indicates fields starting with "f" in `_shards` in `responses`, and `responses.\*\*._score` indicates all `_score` fields in `responses`.

## Request Content
Queries mainly include regular queries and aggregate queries. Query requests are fully compatible with Elasticsearch APIs. For the specific request content, please see the samples.

## Response Content 
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, please see the `error` field description. Some common returned fields for queries are as detailed below. You can set the `filter_path` parameter to simplify the returned query results.

| Field | Description                                                         |
| --------- | ------------------------------------------------------------ |
| hits      | Matched query results. Here, the `total` field indicates the number of matched data records. The `hits` field is an array, which contains the first 10 query results if not specified. Each result in the `hits` array contains `_index` ([child metric](https://intl.cloud.tencent.com/document/product/1100/40909#rolling) involved in the query). If `docvalue_fields` is specified in the query, the `fields` field will be returned to indicate the value of each field. |
| took      | Time in milliseconds taken by the entire query.                                       |
| \_shards  | Number of shards involved in the query. Here, `total` indicates the total number of shards, `successful` the shards that were successfully queried, `failed` the shards that failed to be queried, and `skipped` skipped shards. |
| timed_out | Indicates whether query timed out. Valid values: false, true.                         |
| status    | Status code returned for the query. `2XX` indicates success.                             |

## Sample Code for curl 

**Request without the `filter_path` parameter:**

Request:
```
curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/_msearch -d'
{"index" : "amyli_weather","routing":"host_20"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
{"index" : "ctsdb_test2017","routing":"host_100"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
'
```

Response:
```
{
  	"responses": 
		[
		    {
		      "took": 0,
		      "timed_out": false,
		      "_shards": {
		        "total": 0,
		        "successful": 0,
		        "skipped": 0,
		        "failed": 0
		      },
		      "hits": {
		        "total": 0,
		        "max_score": 0,
		        "hits": []
		      },
		      "status": 200
		    },
		    {
		      "took": 1,
		      "timed_out": false,
		      "_shards": {
		        "total": 3,
		        "successful": 3,
		        "skipped": 0,
		        "failed": 0
		      },
		      "hits": {
		        "total": 1,
		        "max_score": 1,
		        "hits": [
		          {
		            "_index": "ctsdb_test2017@-979200000_30",
		            "_type": "doc",
		            "_id": "AV_8fBhlUAkC9PF9L-2t",
		            "_score": 1
		          }
		        ]
		      },
		      "status": 200
		    }
	  	]
	}
```

**Request with the `filter_path` parameter:**

Request:
```
curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/_msearch?filter_path=responses.\*\*.hits,responses._shards.f\*,-responses.\*\*._score -d'
{"index" : "amyli_weather","routing":"host_20"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
{"index" : "ctsdb_test2017","routing":"host_100"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
'
```

Response:
```
{
  	"responses": [
    {
      "_shards": {
        "failed": 0
      }
    },
    {
      "_shards": {
        "failed": 0
      },
      "hits": {
        "hits": [
          {
            "_index": "ctsdb_test2017@-979200000_30",
            "_type": "doc",
            "_id": "AV_8fBhlUAkC9PF9L-2t"
          }
        ]
      }
    }
  	]
	}
```
>?If both match and filter conditions are set in the `filter_path` parameter, the filter condition will be applied first for the returned results and then the match condition.

