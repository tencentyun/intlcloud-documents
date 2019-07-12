## CacheOptResult

Result of blocking/unblocking URLs

Referenced by: DisableCaches, EnableCaches.

| Name | Type | Description |
|------|------|-------|
| SuccessUrls | Array of String | List of successful URLs <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| FailUrls | Array of String | List of failed URLs <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## CdnData

Detailed access data

Referenced by: DescribeCdnData, DescribeIpVisit, DescribeOriginData.

| Name | Type | Description |
|------|------|-------|
| Metric | String | Query the specified metric: <br/>flux: Traffic (in bytes) <br/>bandwidth: Bandwidth (in bps) <br/>request: Number of requests <br/>fluxHitRate: Traffic hit rate (in %) <br/>statusCode: Status code; return the aggregated data for 2xx, 3xx, 4xx, and 5xx status codes (in entries) <br/>2XX: Return the aggregated list of 2xx status codes and the data for status codes starting with 2 (in entries) <br/>3XX: Return the aggregated list of 3xx status codes and the data for status codes starting with 3 (in entries) <br/>4XX: Return the aggregated list of 4xx status codes and the data for status codes starting with 4 (in entries) <br/>5XX: Return the aggregated list of 5xx status codes and the data for status codes starting with 5 (in entries) <br/>Alternatively, you can specify a specific status code for querying |
| DetailData | Array of [TimestampData](#TimestampData) | Detailed data combination |
| SummarizedData | [SummarizedData](#SummarizedData) | Aggregated data combination |

## MapInfo

Query the mapping between a name and an ID

Referenced by: DescribeMapInfo.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Object ID |
| Name | String | Object name |

## ResourceData

Query an object and its access details

Referenced by: DescribeCdnData and DescribeIpVisit.

| Name | Type | Description |
|------|------|-------|
| Resource | String | Resource name, which is classified as follows based on different query conditions: <br/>A specific domain name: This indicates the details of this domain name <br/>multiDomains: This indicates the aggregated details of multiple domain names <br/>Project ID: This displays the ID of the specifically queried project <br/>all: Details at the account level |
| CdnData | Array of [CdnData](#CdnData) | Data details of a resource |

## ResourceOriginData

Query an object and its origin-pull details

Referenced by: DescribeOriginData.

| Name | Type | Description |
|------|------|-------|
| Resource | String | Resource name, which is classified as follows based on different query conditions: <br/>A specific domain name: This indicates the details of this domain name <br/>multiDomains: This indicates the aggregated details of multiple domain names <br/>Project ID: This displays the ID of the specifically queried project <br/>all: Details at the account level |
| OriginData | Array of [CdnData](#CdnData) | Origin-pull data details |

## SummarizedData

Aggregated values of details; each metric has different aggregation methods based on its characteristics

Referenced by: DescribeCdnData, DescribeIpVisit, DescribeOriginData.

| Name | Type | Description |
|------|------|-------|
| Name | String | Aggregation method, which can be: <br/>sum: Aggregated summation <br/>max: Maximum value; in bandwidth mode, the peak bandwidth is calculated based on the aggregated data with 5-minute granularity <br/>avg: Average value |
| Value | Float | Aggregated data value |

## TimestampData

Timestamp and its corresponding value

Referenced by: DescribeCdnData, DescribeIpVisit, DescribeOriginData.

| Name | Type | Description |
|------|------|-------|
| Time | Timestamp | Statistical point in time in forward rounding mode <br/>Take the 5-minute granularity as an example: 13:35:00 indicates that the statistical interval is between 13:35:00 and 13:39:59 |
| Value | Float | Data value |

## TopData

Data structure of sorted data

Referenced by: ListTopData.

| Name | Type | Description |
|------|------|-------|
| Resource | String | Resource name, which is classified as follows based on different query conditions: <br/>A specific domain name: This indicates the details of this domain name <br/>multiDomains: This indicates the aggregated details of multiple domain names <br/>Project ID: This displays the ID of the specifically queried project <br/>all: Details at the account level |
| DetailData | Array of [TopDetailData](#TopDetailData) | Detailed sorting results |

## TopDetailData

Data structure of sorted data

Referenced by: ListTopData.

| Name | Type | Description |
|------|------|-------|
| Name | String | Datatype name |
| Value | Float | Data value |

## UrlRecord

Details of the blocked URLs

Referenced by: GetDisableRecords.

| Name | Type | Description |
|------|------|-------|
| Status | String | Status (disable: blocked; enable: unblocked) <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RealUrl | String | Corresponding URL <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CreateTime | String | Creation time <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| UpdateTime | String | Update time <br/>Note: This field may return null, indicating that no valid values can be obtained. |

