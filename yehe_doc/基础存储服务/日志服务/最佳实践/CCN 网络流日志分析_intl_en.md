## Overview

[Tencent Cloud Flow Logs (FL)](https://intl.cloud.tencent.com/document/product/682/18931) provides a full-time, full-flow, and non-intrusive traffic collection service. It enables you to store and analyze the collected network traffic in real time for troubleshooting, compliance auditing, architecture optimization, and security detection.

You can create a flow log within the specified collection range (such as ENI, NAT Gateway, and cross-region CCN traffic) to collect inbound/outbound traffic within the range.

## Prerequisites

You have collected [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003) flow logs to Cloud Log Service (CLS). For more information, see [Creating Flow Logs](https://intl.cloud.tencent.com/document/product/682/18966).

## Example

### Using CLS to analyze a CCN flow log

FL is interconnected with CLS, so you can ship CCN flow log data to CLS in real time to further use the search and SQL analysis capabilities of CLS to meet your personalized real-time log analysis needs in different scenarios:

- Push-button log shipping
- Analyzing tens of billions of log data entries within seconds
- Visualizing real-time logs on dashboards
- Real-time alarm reporting in 1 minute


### CCN flow log field description

| Field | Data Type | Description |
| :---------- | :------- | :----------------------------------------------------------- |
| srcaddr     | text     | Source IP.                                                      |
| dstregionid | text     | Traffic destination region.                                               |
| dstport     | long     | Traffic destination port. This field will take effect only for UDP/TCP protocols and will be displayed as "-" for other protocols. |
| start       | long     | The timestamp when the first packet is received in the current capture window. If there are no packets in the capture window, it will be displayed as the start time of the capture window in Unix seconds. |
| dstaddr     | text     | Destination IP.                                                    |
| version     | text     | Flow log version.                                                 |
| packets     | long     | Number of packets transferred in the capture window. This field will be displayed as "-" when `log-status` is `NODATA`. |
| ccn-id      | text     |  Unique CCN instance ID. To get the information of your CCN instance, [contact us](https://intl.cloud.tencent.com/document/product/1003/41737). |
| protocol    | long     | IANA protocol number of the traffic. For more information, see [Assigned Internet Protocol Numbers](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml#protocol-numbers-1). |
| srcregionid | text     | Traffic source region.                                                 |
| bytes       | long     | Number of bytes transferred in the capture window. This field will be displayed as "-" when `log-status` is `NODATA`. |
| action      | text     | Operation associated with the traffic:<ul  style="margin: 0;"><li> ACCEPT: Cross-region traffic normally forwarded over CCN.</li><li>REJECT: Cross-region traffic prevented from being forwarded due to traffic throttling.</li></ul>  |
| region-id   | text     | The region where logs are recorded.                                             |
| srcport     | text     | Traffic source port. This field will take effect only for UDP/TCP protocols and will be displayed as "-" for other protocols. |
| end         | long     | The timestamp when the last packet is received in the current capture window. If there are no packets in the capture window, it will be displayed as the end time of the capture window in Unix seconds. |
| log-status  | text     | Logging status of the flow log. Valid values:<ul  style="margin: 0;"><li> OK: Data is normally logged to the specified destination.</li><li> NODATA: There was no inbound or outbound network flow in the capture window, in which case both the `packets` and `bytes` fields will be displayed as `-1`.</li></ul>  |



### CCN access analysis

#### Background

To better manage your business, you can adjust the bandwidth cap in each region at any time. In this case, you need to monitor and collect the cross-region bandwidth and set bandwidth usage alerts.

<dx-accordion>
::: Bandwidth trend of each line
```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(bytes)/60.00*8 as bandwidth, concat(concat('srcRegion : ',srcregionid, ' , dstRegion : '), dstregionid) as region_ip group by time, region_ip limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/90b634a3d1efe7cf107d35cd60a4f341.png)
:::
::: PPS trend of each line

```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(packets)/60.00 as pps, concat(concat('srcRegion : ',srcregionid, ' , dstRegion : '), dstregionid) as region_ip group by time, region_ip limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/00e763ba49323953a55c82301a8a2b15.png)

:::
::: Total traffic distribution of top 20 lines

```sql
log-status:OK | select concat(concat('srcRegion : ',srcregionid, ' , dstRegion : '), dstregionid) as region, sum(bytes) as bytes group by region order by bytes desc limit 20
```

![](https://qcloudimg.tencent-cloud.cn/raw/eb4ec3396c44b6d2a6dc228823205aca.png)

:::
::: Traffic bandwidth of top 10 source IPs
```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(bytes)/60.00*8 as pps  , srcaddr where srcaddr in (select srcaddr group by srcaddr order by sum(cast(bytes as double)) desc limit 10)  group by time, srcaddr limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/016fa7fcbcd82a8adc9432248cfb0241.png)

:::
::: Traffic PPS of top 10 source IPs

```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(packets)/60.00 as pps  , srcaddr where srcaddr in (select srcaddr group by srcaddr order by sum(cast(packets as double)) desc limit 10) group by time, srcaddr  limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/492c4137a8b8175b0bd2e6df9804bdfe.png)

:::
::: Traffic bandwidth of top 10 protocols
```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(bytes)/60*8 as bandwidth, cast(protocol as varchar) where protocol in ( select protocol group by protocol order by sum(cast(bytes as double)) desc limit 10) group by time, protocol  limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/067cf27370901b8cfc3da20879f8a445.png)

:::
::: Traffic PPS of top 10 protocols
```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(packets)/60.00 as pps, cast(protocol as varchar) where protocol in ( select protocol group by protocol order by sum(cast(bytes as double)) desc limit 10) group by time, protocol  limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/afe57e19f895ff8f1d27a4fc73183369.png)

:::
::: Proportion of denied access requests
```sql
log-status:OK | select round(sum(case when action = 'REJECT' then 1.00 else 0.00 end) / cast(count(*) as double) * 100,2) as "Proportion of denied access requests (%)"
```

![](https://qcloudimg.tencent-cloud.cn/raw/07b0c0a5df6c833771c90b6d75d7185f.png)

:::
::: Bandwidth trend of `ACCEPT` and `REJECT`
```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(bytes)/60.00*8 as bandwidth, action group by time, action limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/d660929f56275b9f4cf47c0119a8030a.png)

:::
::: PPS of `ACCEPT` and `REJECT`
```sql
log-status:OK | select histogram(cast(__TIMESTAMP__ as timestamp), interval 1 MINUTE) as time, sum(packets)/60.00 as pps, action group by time, action limit 10000
```

![](https://qcloudimg.tencent-cloud.cn/raw/ca2ca83521267a6ba1e979c673b1e236.png)

:::
::: Bandwidth threshold alarm of a line
During business operations, you configure a bandwidth cap for a line, and then you need to monitor the reasonableness of the configuration and adjust the cap for a region at any time to better control the network connectivity. For example, the bandwidth cap of the Hong Kong (China) - Silicon Valley line is set to 100 Mbps at first; if the bandwidth usage of the line stays equal to or greater than 95 Mbps for over ten minutes, an alarm will be triggered for you to adjust the cap in time.

Configure a CLS alarm based on the above scenario.

1. Create a monitoring task, enter the following query statement, and select one minute for the time range to collect the bandwidth usage of the Hong Kong (China) - Silicon Valley line in the past minute once every minute:
```sql
log-status:OK AND srcregionid:ap-hongkong AND dstregionid:na-siliconvalley | select sum(bytes)/60.00*8/1000 as bandwidth
```

2. Configure an alarm policy to trigger an alarm if ten consecutive results of the monitoring task are all equal to or greater than 95 Mbps.


:::
</dx-accordion>
