#### Request address

The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

#### Request path and method

Path: `/_metric/${metric_name}`, where `${metric_name}` is the name of the metric to be deleted.
Method: DELETE

#### Request parameters

None

#### Request content

None

#### Response content

You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, see the `error` field description.

#### Sample code for curl

Request:
`DELETE /_metric/ctsdb_test1`
Request:
`curl -u root:le201909 -H 'Content-Type:application/json' -X DELETE 172.16.345.14:9201/_metric/ctsdb_test1`

Response:

```
{
   "acknowledged": true,
   "message": "delete metric ctsdb_test1 success!"
}
```
