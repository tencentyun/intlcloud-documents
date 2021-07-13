
CTSDB supports data write, query, and other operations over the HTTP protocol. Its HTTP APIs are RESTful, and the resource request method is to send standard HTTP requests to the corresponding URIs of resources. For example, `GET` is used to get resources, `POST` create (or update) resources, `PUT` update resources, and `DELETE` delete resources.

You can perform almost all data operations through HTTP APIs. CTSDB ensures data security by providing VPC-based network isolation and access authentication with username and password. Data is exchanged through structures in JSON format. Each request will return a standard HTTP response status code and content. If an operation fails, you can get specific error information based on the response content.

For more information on how to connect to instances through RESTful API, please see [Connecting to Instance](https://intl.cloud.tencent.com/document/product/1100/40928).

## Naming Conventions 
The names of metrics, tags, and fields in CTSDB should be concise and clear. For more information on tags and fields, please see [Request Content](https://intl.cloud.tencent.com/document/product/1100/40909):
- **Naming conventions for metrics**: a name can contain 1–200 lowercase letters, digits, underscores, hyphens, and dots but cannot start with a dot, underscore, or hyphen.
- **Naming conventions for tags and fields in metrics**: a name can contain 1–255 letters, digits, underscores, hyphens, and dots but cannot start with a dot.

## System Limits 
- **Limits of tags and fields in metrics**: the total number of fields in a metric cannot exceed 1,000.
- **Limits of write points during bulk writing to metric**: we recommend you limit the number of records in each `bulk` request between 1,000 and 5,000 and the physical size between 1 and 15 MB.

## System Default Rules 
- **Processing of new fields during data write**: if there are undefined new fields when you write data to a metric, CTSDB will store the new fields as tags by default. You can also change this by modifying the `default_type` field in the `options` parameter of the metric. For more information on metric modification, please see [Updating Metric](https://intl.cloud.tencent.com/document/product/1100/40907).
 - If a new field is an integer, CTSDB will store it in `long` type.
 - If a new field is a decimal number, CTSDB will store it in `float` type.
 - If a new field is a string, CTSDB will store it in `string` type subject to the value of `max_string_length` and discard the excessive part. `max_string_length` can be customized and is 256 characters by default. For more information on modification, please see [Updating Metric](https://intl.cloud.tencent.com/document/product/1100/40907).
- **Processing of date and time**: date and time are stored in UTC format in CTSDB. Therefore, for data queries involving time range, please specify the time zone with the `time_zone` parameter, which is in the format of ISO 8601 UTC offset (e.g., +01:00 or -08:00). The specific time zone needs to be determined according to the region where the instance resides. Generally, the time zone for the Chinese mainland is UTC+8. For more information, please see [Common Query Samples](https://intl.cloud.tencent.com/document/product/1100/40902).

## Instance Connection
CTSDB instances currently can be connected to only in VPCs. You can connect to an instance in the console or through RESTful APIs. In the latter case, you need to provide the root account password to ensure security.

Below is a code sample for connecting to an instance and creating a metric through curl. Here, `${user:password}` is the username and password of the instance, `${vip}:${vport}` the IP and port, and `${metric_name}` the name of the created metric.

```
curl -u ${user:password} -H 'Content-Type:application/json' -X PUT ${vip}:${vport}/_metric/${metric_name} -d'
{ 
    "tags": {
        "region": "string",
        "set":  "long",
        "host": "string"
    },
    "time": {
         "name": "timestamp",
         "format": "epoch_second"
    },
    "fields": {
        "cpu_usage":  "float"
    },
    "options": {
        "expire_day": 7,
        "refresh_interval": "10s",
        "number_of_shards": 5,
        "number_of_replicas": 1,
        "rolling_period": 1
    }
}'
```
