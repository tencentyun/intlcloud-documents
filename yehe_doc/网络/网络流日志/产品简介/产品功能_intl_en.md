Flow Logs (FL) service provides log collection, query, data management and record features, helping you easily perform OPS and quickly troubleshoot issues.

## Flow Log Collection

After a flow log is created for an ENI, the log stream of the ENI will be automatically collected and the log data will be synced to [CLS](https://intl.cloud.tencent.com/document/product/614/11254). In the CLS topic, each ENI has a unique log stream which contains flow log records.

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
|srcport | Source port of the traffic. This field indicates the ICMP ID for ICMP traffic.|
|dstport | Destination port of the traffic. This field indicates a combination of IMCP type (bits 0-7) and code (bits 8-15) for ICMP traffic. |
| protocol | IANA protocol number of the traffic. For more information, see the [Assigned Internet Protocol Numbers](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml#protocol-numbers-1). |
| packets | Number of packets transferred in the capture window. |
| bytes | Number of bytes transferred in the capture window. |
| start | Start time of the capture window in Unix seconds. |
| end | End time of the capture window in Unix seconds. |
|action | Traffic-related action. Valid values: <br/>ACCEPT: the traffic allowed by the security group or network ACL. <br/>REJECT: the traffic rejected by the security group or network ACL. |
|log-status | Logging status of the flow log. Valid values:<br>OK: data is logging normally to the specified destination.<br/>NODATA: there was no incoming or outgoing network flow in the capture window. In this case, both `packets` and `bytes` fields are displayed as `-1`.<br/>SKIPDATA: some flow log records were skipped in the capture window. This may be caused by an internal capacity constraint or an internal error. |


### Samples
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
  If your network ACL allows the inbound but rejects the outbound ICMP traffic, response to the ping request will be discarded and will not be sent to your home computer as the network ACL is stateless. In this case, the flow log has two records:
  - The ACCEPT record for sending the ping command allowed by both network ACL and security group (so that the traffic can reach your instance).
  - The REJECT record for the response to the ping command rejected by the network ACL.

  ```
  V1 1251762227 eni-lq6mkcis 203.0.113.12 172.31.16.139 0 0 1 4 336 1432917027 1432917142 ACCEPT OK
  ```

  ```
  V1 1251762227 eni-lq6mkcis 172.31.16.139 203.0.113.12 0 0 1 4 336 1432917094 1432917142 REJECT OK
  ```

  If your network ACL allows the outbound ICMP traffic, your flow log will have two ACCEPT records (one for sending the ping command and the other for responding). If your security group rejects the inbound ICMP traffic and the traffic does not reach your instance, the flow log has one REJECT record.
