Flow Logs (FL) service provides log collection, query, data management and record features, helping you easily perform OPS and quickly troubleshoot issues.

## Flow Log Collection

After a flow log is created for an ENI, the log stream of the ENI will be automatically collected and the log data will be synced to [CLS](https://intl.cloud.tencent.com/document/product/614/11254). In the CLS topic, each ENI has a unique log stream which contains log flow records.

## Flow Log Query
[CLS](https://intl.cloud.tencent.com/document/product/614/11254) supports querying hundreds of millions of log data entries. You can search for data with full text or multiple keywords across topics, and the results can be returned within seconds.

## Flow Log Data
FL integrates with [CLS](https://intl.cloud.tencent.com/document/product/614/11254) to store and manage log data.

## Flow Log Record
A flow log records the network flow that passes through the capture window and matches the 5-tuple rules.

- **5-tuple**
It refers to a collection of five values: source IP address, source port, destination IP address, destination port, and transport layer protocol.
- **Capture window**
It refers to a time period of 5 to 10 minutes, during which FL aggregates data and takes about 5 minutes to publish the flow log records. Flow log records are strings separated with spaces as the following format:
`version account-id interface-id srcaddr dstaddr srcport dstport protocol packets bytes start end action log-status`

| Field | Description |
|---------|---------|
| version | FL version. |
| account-id | AppID of the FL account.|
| interface-id | ENI ID. |
| srcaddr | Source IP. |
| dstaddr | Destination IP. |
| srcport | Source port of the traffic. |
| dstport | Destination port of the traffic. |
| protocol | IANA protocol number of the traffic. For more information, see the assigned [Internet Protocol Numbers](https://www.iana.org/numbers). |
| packets | Number of packets transferred in the capture time window. |
| bytes | Number of bytes transferred in the capture time window. |
| start | Start time of the capture time window in Unix seconds. |
| end | End time of the capture time window in Unix seconds. |
|action | Traffic-related action. Valid values: <br/>ACCEPT: the traffic allowed by the security group or network ACL is collected. <br/>REJECT: the traffic rejected by the security group or network ACL is collected. |
| log-status | Flow log status. Valid values: <br/>OK: data is collected and saved to the specified destination.<br/>NODATA: there was no network traffic passing through the ENI in the capture time window.<br/>SKIPDATA: some flow log records were skipped in the capture time window due to internal capacity constraint or an internal error. |


### Examples
- The following sample flow log indicates that SSH traffic (destination port: 22, TCP protocol) was allowed to be directed to the `eni-lq6mkcis` ENI under the `1251762227` account.

  ```
  2 1251762227 eni-lq6mkcis 172.31.16.139 172.31.16.21 20641 22 6 20 4249 1418530010 1418530070 ACCEPT OK
  ```

- The following sample flow log indicates that the RDP traffic (destination port: 3389, TCP protocol) was rejected to be directed to the `eni-lq6mkcis` ENI under the `1251762227` account.

  ```
  2 1251762227 eni-lq6mkcis 172.31.9.69 172.31.9.12 49761 3389 6 20 4249 1418530010 1418530070 REJECT OK
  ```

- The following sample flow log indicates that no data was collected in the capture time window:

  ```
  V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - NODATA
  ```

- The following flow log indicates that some data was skipped in the capture time window:

  ```
  V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - SKIPDATA
  ```

- Flow log record of security group and network ACL rules

  Security group is stateful, which allows response to the accepted traffic. In contrast, network ACL is stateless, which requires that response to the accepted traffic also follow the network ACL rules.

  Assume that you ping your instance (private IP of the network interface: 172.31.16.139) from your home computer (IP: 203.0.113.12). If the security group's inbound rule allows the ICMP traffic, but its outbound rule does not, your instance still responds as the security group is stateful.
  If your network ACL allows the inbound but rejects the outbound ICMP traffic, your instance will not respond as the network ACL is stateless. In this case, the flow log has two records:
  - The ACCEPT record for sending the ping command allowed by both network ACL and security group (so that the traffic can reach your instance).
  - The REJECT record for the response to ping command rejected by the network ACL.

  ```
  V1 1251762227 eni-lq6mkcis 203.0.113.12 172.31.16.139 0 0 1 4 336 1432917027 1432917142 ACCEPT OK
  ```

  ```
  V1 1251762227 eni-lq6mkcis 172.31.16.139 203.0.113.12 0 0 1 4 336 1432917094 1432917142 REJECT OK
  ```

  If the network ACL allows the outbound ICMP traffic, your flow log will have two ACCEPT records (one for sending the ping command and the other for responding). If your security group rejects the inbound ICMP traffic and the traffic does not reach your instance, the flow log has one REJECT record.
