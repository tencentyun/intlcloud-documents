Flow Logs (FL) service provides log collection, query, data management, data record, and analysis features, helping you easily perform Ops and quickly troubleshoot issues.

## Flow Log Collection
After a flow log is created, the log stream in the specified range (such as ENI, NAT Gateway, or cross-region CCN traffic) will be automatically collected, and the log data will be delivered to [CLS](https://intl.cloud.tencent.com/document/product/614/11254) for storage. In the CLS topic, each ENI has a unique log stream which contains flow log records.
>?The FL service for NAT Gateway and cross-region CCN traffic is currently in beta. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Flow Log Query
Flow logs are queried and consumed in [CLS](https://intl.cloud.tencent.com/document/product/614/11254). CLS supports querying hundreds of millions of log data entries. You can search for data with full text or multiple keywords across topics, and the results can be returned within seconds.

## Flow Log Storage
FL integrates with [CLS](https://intl.cloud.tencent.com/document/product/614/11254) to store and manage log data.

## Creating Dashboard to Display Log Data in Multiple Dimensions
In the logset "flowlog_logset" dedicated to flow logs, you can create a dashboard for ENI flow logs to visualize and analyze flow log data. One dashboard can be created for each log topic.
Data display in the dashboard is as shown below. For more information, see [Advanced Analysis](https://intl.cloud.tencent.com/document/product/682/47039).
![]()

## Flow Log Record
A flow log records the network flow that passes through the capture window and matches particular rules.

<dx-tabs>
::: Flow log records of cross-region CCN traffic
The flow logs record the network flows filtered by the "quintuple + traffic source region + traffic destination region" rule in a specific capture window; that is, only flow logs that meet the rule in the capture window can be recorded as flow logs of cross-region CCN traffic.

- **Quintuple + traffic source region + traffic destination region**
  - A quintuple refers to a collection of five values: source IP address, source port, destination IP address, destination port, and transport layer protocol.
  - The traffic source region refers to the region from which cross-region CCN traffic is sent.
  - The traffic destination region refers to the region to which cross-region CCN traffic arrives.
- **Capture window**
It refers to the time period during which FL takes 1 minute to aggregate data and takes about 5 minutes to publish the flow log records. Flow log records are strings separated with spaces as the following format:
`srcaddr dstregionid dstport start dstaddr version packets ccnid protocol srcregionid bytes action region-id srcport end log-status`

| Field | Data Type | Description |
|---------|--------- |---------|
|srcaddr |text | Source IP. |
|dstregionid | text | Traffic destination region. |
|dstport | long | Traffic destination port. This field will take effect only for UDP/TCP protocols and will be displayed as "-" for other protocols. |
|start | long | The timestamp when the first packet is received in the current capture window. If there are no packets in the capture window, it will be displayed as the start time of the capture window in Unix seconds. |
|dstaddr | text| Destination IP. |
|version | text | Flow log version. |
|packets |long | Number of packets transferred in the capture window. This field will be displayed as "-" when `log-status` is `NODATA`. |
|ccn-id |text  | Unique CCN instance ID. To get the information of your CCN instance, [contact us](https://intl.cloud.tencent.com/document/product/1003/41737). |
|protocol | long | IANA protocol number of the traffic. For more information, see [Assigned Internet Protocol Numbers](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml#protocol-numbers-1). |
|srcregionid | text | Traffic source region. |
|bytes | long | Number of bytes transferred in the capture window. This field will be displayed as "-" when `log-status` is `NODATA`. |
|action | text	 | Operation associated with the traffic:<br/> ACCEPT: Cross-region traffic normally forwarded over CCN.<br/>  REJECT: Cross-region traffic prevented from being forwarded due to traffic throttling. |
|region-id | text| Region where logs are recorded. |
|srcport |text  | Traffic source port. This field will take effect only for UDP/TCP protocols and will be displayed as "-" for other protocols. |
|end | long | The timestamp when the last packet is received in the current capture window. If there are no packets in the capture window, it will be displayed as the end time of the capture window in Unix seconds. |
|log-status | text | Logging status of the flow log. Valid values:<br>OK: Data is normally logged to the specified destination.<br/>NODATA: There was no inbound or outbound network flow in the capture window, in which case both the `packets` and `bytes` fields will be displayed as `-1`. |

::: 
::: Flow log records of other types
A flow log records the network flow that passes through the capture window and matches the quintuple rules.

- **Quintuple**
It refers to a collection of five values: source IP address, source port, destination IP address, destination port, and transport layer protocol.
- **Capture window**
It refers to the time period during which FL takes around 5 minutes to aggregate data and takes about 5 minutes to publish the flow log records. Flow log records are strings separated with spaces as the following format:
`version account-id interface-id srcaddr dstaddr srcport dstport protocol packets bytes start end action log-status`


| Field | Description |
|---------|---------|
| version | FL version. |
| account-id | AppID of the FL account.|
| interface-id | ENI ID. |
| srcaddr | Source IP. |
| dstaddr | Destination IP. |
|srcport | Source port of the traffic. This field indicates the ICMP ID for ICMP traffic.|
|dstport | Destination port of the traffic. This field indicates a combination of ICMP type (bits 0-7) and code (bits 8-15) for ICMP traffic. |
| protocol | IANA protocol number of the traffic. For more information, see the [Assigned Internet Protocol Numbers](). |
| packets | Number of packets transferred in the capture window. |
| bytes | Number of bytes transferred in the capture window. |
| start | Start time of the capture window in Unix seconds. |
| end | End time of the capture window in Unix seconds. |
|action | 	Traffic-related action. Valid values: <br/>ACCEPT: the traffic allowed by the security group or network ACL. <br/>REJECT: the traffic rejected by the security group or network ACL. |
|log-status | Logging status of the flow log. Valid values:<br>OK: data is logging normally to the specified destination.<br/>NODATA: there was no incoming or outgoing network flow in the capture window. In this case, both `packets` and `bytes` fields are displayed as `-1`.<br/>SKIPDATA: some flow log records were skipped in the capture window. This may be caused by an internal capacity constraint or an internal error. |

### Example
- The flow log recorded when the SSH traffic (destination port: 22; TCP) of the ENI `eni-lq6mkcis` under the account `1251762227` was accepted:
  ```
  2 1251762227 eni-lq6mkcis 172.31.16.139 172.31.16.21 20641 22 6 20 4249 1418530010 1418530070 ACCEPT OK
  ```
- The flow log recorded when the RDP traffic (destination port: 3389; TCP) of the ENI `eni-lq6mkcis` under the account `1251762227` was rejected:
  ```
  2 1251762227 eni-lq6mkcis 172.31.9.69 172.31.9.12 49761 3389 6 20 4249 1418530010 1418530070 REJECT OK
  ```
- The flow log recorded when there was no data collected in the capture window:
  ```
  V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - NODATA
  ```
- The flow log recorded when there was data skipped in the capture window:
  ```
  V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - SKIPDATA
  ```
- Flow log record of security group and network ACL rules:
   - The security group is stateful; therefore, it allows response to the accepted traffic.
   - The network ACL is stateless; therefore, the response to the accepted traffic should follow the network ACL rules.

  For example, if you ping your instance (private IP of the network interface: 172.31.16.139) from your home computer (IP: 203.0.113.12), and the security group's inbound rule allows the ICMP traffic while its outbound rule does not, your instance will respond to the ping command as the security group is stateful.
  If your network ACL allows the inbound but rejects the outbound ICMP traffic, response to the ping command will be discarded and will not be sent to your home computer as the network ACL is stateless. In this case, the flow log has two records:
   - The ACCEPT record for sending the ping command allowed by both network ACL and security group (so that the traffic can reach your instance).
   - The REJECT record for the response to the ping command rejected by the network ACL.

  ```
  V1 1251762227 eni-lq6mkcis 203.0.113.12 172.31.16.139 0 0 1 4 336 1432917027 1432917142 ACCEPT OK
  ```

  ```
  V1 1251762227 eni-lq6mkcis 172.31.16.139 203.0.113.12 0 0 1 4 336 1432917094 1432917142 REJECT OK
  ```

  If your network ACL allows the outbound ICMP traffic, your flow log will have two ACCEPT records (one for sending the ping command and the other for responding). If your security group rejects the inbound ICMP traffic and the traffic does not reach your instance, the flow log has one REJECT record.
::: 
</dx-tabs>
