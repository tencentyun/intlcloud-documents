## Connection limitations
Note the following when you use a peering connection:
- To enable real communication between both ends of a peering connection, you must configure routing rules in the route tables of both the sending and receiving ends.
- The fee for a cross-region peering connection is paid by the requester of the connection.
- If the acceptor does not accept a peering connection request, the request will automatically expire after 7 days.
- Do not accept peering connection requests from unknown accounts because they may pose risks to your network.
- The VPC CIDR blocks on both ends of a peering connection cannot overlap. Otherwise, an error will occur when the connection is connected.
- For a cross-region peering connection, the CIDR blocks of multiple peer networks of one VPC cannot overlap. Otherwise, an error will occur.
- Either end of a peering connection can interrupt the connection. Then, traffic between the two VPCs is disconnected immediately.
- There is no bandwidth cap for an intra-region peering connection, and a bandwidth cap must be set for a cross-region peering connection.

## Resource limitations

| Resource | Limitation | Description |
| -------------- | ----- | -------------------------------- |
| Bandwidth cap for a cross-region peering connection | 1 Gbps | The bandwidth cap for an intra-region peering connection is 5 Gbps.<br/>If you need higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). |
| Max number of peering connections supported by each VPC | 10 | - |


For more information, see [other service limitations on a VPC](https://intl.cloud.tencent.com/document/product/215/537).
