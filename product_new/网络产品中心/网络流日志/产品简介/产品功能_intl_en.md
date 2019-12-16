## Collecting Flow Logs
You can create a flow log for an ENI. The flow log data can be published to a topic in CLS. Each ENI has a unique log stream which contains flow log records.
## Querying Flow Logs
You can query flow logs in CLS. Features such as full-text search, multi-keyword search, and cross-topic query are supported. Query results can be returned within seconds. Hundreds of millions of log data entries can be searched for with ease.
## Publishing Flow Log Data
- **Publishing to [COS](https://intl.cloud.tencent.com/document/product/436)**
CLS can publish the flow log data to a COS bucket under your account to store and manage such data.

## Flow Log Record
A flow log record represents a network flow in your flow logs. Each record captures a particular 5-tuple network flow that occurs within a capture window.
- **5-tuple**
It refers to the source, destination, and protocol.
- **Capture window**
The capture window is a period of 5 to 10 minutes, during which all flows of data are aggregated and published. The publishing period is about 5 minutes. A flow log record is a space-separated string in the following format:
version account-id interface-id srcaddr dstaddr srcport dstport protocol packets bytes start end action log-status

| Field | Description | 
|---------|---------|
| version | Flow log version. |
| account-id | AppID of the flow log account. |
| interface-id | ENI ID. |
| srcaddr | Source IP. |
| dstaddr | Destination IP. |
| srcport | Source port of the traffic. |
| dstport | Destination port of the traffic. |
| protocol | IANA protocol number of the traffic. For more information, see the assigned [Internet Protocol Numbers](http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml). |
| packets | Number of packets transferred in the capture window. |
| bytes | Number of bytes transferred in the capture window. |
| start | Start time of the capture window in Unix seconds. |
| end | End time of the capture window in Unix seconds. |
|action | Action associated with the traffic. <br/> ACCEPT: The recorded traffic was permitted by the security groups or network ACLs. <br/>  REJECT: The recorded traffic was not permitted by the security groups or network ACLs. |
| log-status | Logging status of the flow log. <br/>OK: Data is logging normally to the specified destination. <br/>NODATA: There was no network traffic passing through the ENI in the capture window. <br/>SKIPDATA: Some flow log records were skipped in the capture window. This may be caused by an internal capacity constraint or an internal error. | 


### Example: flow log record
#### Flow log record for accepted traffic
The following is an example of a flow log record, which records the SSH traffic permitted to be directed to the ENI `eni-lq6mkcis` under the account `1251762227` (destination port: 22; protocol: TCP).
```
2 1251762227 eni-lq6mkcis 172.31.16.139 172.31.16.21 20641 22 6 20 4249 1418530010 1418530070 ACCEPT OK
```

#### Flow log record for rejected traffic
The following is an example of a flow log record, which records the RDP traffic rejected to be directed to the ENI `eni-lq6mkcis` under the account `1251762227` (destination port: 3389; protocol: TCP).
```
2 1251762227 eni-lq6mkcis 172.31.9.69 172.31.9.12 49761 3389 6 20 4249 1418530010 1418530070 REJECT OK
```

#### Flow log record for no data
The following is an example of a flow log record where no data is recorded in the capture window.
```
V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - NODATA
```

#### Flow log record for skipped data

The following is an example of a flow log record which is skipped in the capture window.
```
V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - SKIPDATA
```
#### Security group and network ACL rules
Security group is stateful, that is, response to the accepted traffic is also permitted. In contrast, network ACL is stateless, that is, response to the accepted traffic must follow the network ACL rules.

For example, when you ping your instance (private IP of the network interface: 172.31.16.139) from your home computer (IP: 203.0.113.12), if the security group's inbound rule permits ICMP traffic, but its outbound rule does not, then response from your instance to the ping request is permitted as the security group is stateful.
Supposing that your network ACL permits inbound ICMP traffic but not outbound ICMP traffic, as the network ACL is stateless, response to the ping request will be discarded and will not be sent to your home computer. The following two flow log records will be displayed in the flow log:
- The ACCEPT record for the initiation of the ping request permitted by both network ACL and security group (so that the traffic can reach your instance).
- The REJECT record for the response to the ping request rejected by the network ACL.
 ```
V1 1251762227 eni-lq6mkcis 203.0.113.12 172.31.16.139 0 0 1 4 336 1432917027 1432917142 ACCEPT OK
```
```
V1 1251762227 eni-lq6mkcis 172.31.16.139 203.0.113.12 0 0 1 4 336 1432917094 1432917142 REJECT OK
```

If the network ACL permits outbound ICMP traffic, two ACCEPT records (one for initiating the ping request and the other for responding to the ping request) will be displayed in your flow log. If your security group rejects inbound ICMP traffic, a REJECT record will be displayed in the flow log, because the traffic does not reach your instance.
