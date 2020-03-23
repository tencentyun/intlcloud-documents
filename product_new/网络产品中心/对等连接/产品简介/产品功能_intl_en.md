## Non-transitive connectivity of peering connections
A peering connection enables connectivity between two VPCs, but the connectivity cannot be transited.
For example, as shown in the following figure, peering connections are created between VPC 1 and VPC 2, and between VPC 1 and VPC 3. However, due to the non-transitivity of peering connections, traffic cannot flow between VPC 2 and VPC 3.
![](https://main.qcloudimg.com/raw/4d0523663c58e3fd6f2f8a88daefea63.jpg)

>**Note:**
>Even if a peering connection is created, both ends of the connection cannot communicate with each other if routes for sending and returning packets are not configured at both ends.

## Intra-region and cross-region peering connections
VPCs support both intra-region and cross-region peering connections. Due to differences in physical distance and underlying implementation architecture, there are some differences between the two types of connections, as shown in the following table:

| Comparison item | Intra-region peering connection | Cross-region peering connection |
| ----- | ----------------------------------- | ---------------------------------------- |
| Underlying architecture | Local private network within a single region based on Tencent Cloud | Cross-region internal MPLS network based on Tencent Cloud |
| Bandwidth | Maximum bandwidth for interconnection with public cloud: 5 Gbps<br/>Maximum bandwidth for interconnection with BM network: 1 Gbps | Maximum bandwidth: 1 Gbps, with the following options available for the bandwidth cap (MB/sec): <br/>10, 20, 50, 100, 200, 500, and 1000 <br/>For peering connections between Beijing, Shanghai, Guangzhou, Korea, and Hong Kong (China), you can [apply for higher bandwidth](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC).<br/>If you require data connectivity between Mainland China and other regions, consult your business manager. |
| Billing | Free of charge | Daily billing based on the regions where the two ends of the peering connection are located and the actual network bandwidth used. For more information, see [Price overview](https://intl.cloud.tencent.com/document/product/215/3079). |
| Availability | Intra-region service quality level: gold; guaranteed availability: ≥ 99.50% | Linkage availability:<br/>Platinum: 99.95%<br/>Gold: 99.50%<br/>Silver: 99.00%<br/>For more information, see [SLA](https://intl.cloud.tencent.com/document/product/215/17800). |
| Cross-account connection | Supported | Supported |
| Access permission | The CVMs at either end of a peering connection can access all the resources at the peer end, including CVMs, databases, and CLBs. | The CVMs at either end of a peering connection can access all the resources at the peer end, including CVMs, databases, and CLBs. |
| Function limits | The VPC IP ranges to which the two ends of a peering connection belong cannot overlap.<br/>Peering connections are independent of each other. | The VPC IP ranges to which the two ends of a peering connection belong cannot overlap.<br/>**If multiple peer VPCs are connected to the same VPC, the IP ranges to which these peer VPCs belong cannot overlap.** |
| Application scenario | Connect applications in different VPCs within the same region | Typical application scenario: **cross-region disaster recovery**<br/>VPCs in different regions can communicate with each other over cross-region peering connections, which helps rapidly deploy a 2-region-3-DC solution for disaster recovery and meet the requirement for financial-level network disaster recovery with high bandwidth and reliability. |

