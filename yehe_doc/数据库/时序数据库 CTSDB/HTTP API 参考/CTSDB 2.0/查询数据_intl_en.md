#### Request address

The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

#### Request path and method

Path: `${metric_name}/_search`, where `${metric_name}` is the metric name.
Method: GET

#### Request parameters

You can set the `_routing` parameter during data write to improve the query efficiency. For more information, see the samples.

#### Request content

Queries mainly include regular queries and aggregate queries. Query requests are fully compatible with [Elasticsearch APIs](https://www.elastic.co/guide/en/elasticsearch/reference/7.10/getting-started.html). For the specific request content, see the samples.

#### Response content

You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, see the `error` field description.

#### Sample code for curl

For specific query samples, see [Common Query Samples](https://intl.cloud.tencent.com/document/product/1100/45518).

