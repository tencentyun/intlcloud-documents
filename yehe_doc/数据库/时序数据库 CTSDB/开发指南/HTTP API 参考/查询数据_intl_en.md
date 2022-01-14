
## Request Address
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

## Request Path and Method
Path: `${metric_name}/_search`, where `${metric_name}` is the metric name.
Method: GET

## Request Parameters 

You can set the `_routing` parameter during data write to improve the query efficiency. For more information, please see the samples.

## Request Content

Queries mainly include regular queries and aggregate queries. Query requests are fully compatible with [Elasticsearch APIs](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/getting-started.html). For the specific request content, please see the samples.

## Response Content 
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, please see the `error` field description.

## Sample Code for curl
For specific query samples, please see [Common Query Samples](https://intl.cloud.tencent.com/document/product/1100/40902).
