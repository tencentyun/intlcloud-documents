## Connection Limits
Please note the following when using peering connection:
- To enable real communication between both ends of a peering connection, you must configure routing rules in route tables of both the sending and receiving ends.
- Costs for cross-region peering connection are paid by the requester of such connection.
- If the other party does not accept a peering connection request, the request will automatically expire after 7 days.
- Please do not accept peering connection requests from unknown accounts because they may pose risks to your network.
- The VPC CIDR on both ends of a peering connection cannot overlap, otherwise an error will occur when you create the connection.
- For a cross-region peering connection, the CIDRs of multiple peer networks of one VPC cannot overlap, otherwise an error will occur.
- Any party of a peering connection can interrupt the connection at any time. The transfer between the two VPC is blocked immediately after the interruption.
- There is no bandwidth limit for intra-region peering connection, and a bandwidth limit must be set for cross-region peering connections.

## Resource Limits

| Resource | Limit | Description |
| -------------- | ----- | -------------------------------- |
| Bandwidth limit for cross-region peering connection |  1 Gbps | The bandwidth cap of the intra-region peering connection is 5 Gbps.<br/>If you need a larger bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category) |
| Number of peering connections supported by each VPC | 10    |                   -               |


For more service restrictions on VPCs, see [Limitations](/document/product/215/537).

