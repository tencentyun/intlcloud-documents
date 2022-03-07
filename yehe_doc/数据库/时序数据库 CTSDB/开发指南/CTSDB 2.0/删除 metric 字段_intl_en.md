## Deleting Metric Field

- [Request address](hyperlink)
- [Request path and method](hyperlink)
- [Request parameters](hyperlink)
- [Request content](hyperlink)
- [Response content](hyperlink)
- [Sample code for curl](hyperlink)

#### Request address

The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

#### Request path and method

Path: `/_metric/${metric_name}/delete`, where `${metric_name}` is the metric name.
Method: PUT

#### Request parameters

None

#### Request content

| Parameter | Required | Type  | Description                                                |
| :------- | :--- | :---- | :-------------------------------------------------- |
| tags     | No   | Array | Enumeration of the tag fields to be deleted, such as `"tags": ["ip"]`          |
| fields   | No   | Array | Enumeration of the data fields to be deleted, such as `"fields": ["diskUsage"]` |

> Note:
>
> As historical data cannot be modified, after fields are deleted, the metric information will not change until the next [child metric](hyperlink) is generated. If you want to check whether the deletion is successful, you can call the `GET /_metric/${metric_name}?v` API.

#### Response content

You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, see the `error` field description.

#### Sample code for curl

Request:

```
curl -u root:le201909 -H 'Content-Type:application/json' -X PUT 172.16.345.14:9201/_metric/ctsdb_test1/delete -d'
{
"tags": ["ip"],        
"fields": ["cpu"]   
}'
```

Response:

```
{
   "acknowledged": true,
   "message": "update ctsdb_test1 metric success!"
}
```
