### Use Limits
- The default route table of each VPC cannot be deleted.
- After creating a VPC, the system automatically adds a default route to the route table, indicating that all resources in this VPC are interconnected through the private network. This routing policy cannot be modified or deleted.
<table><tbody>
<tr><th>Destination</th><th>Next-hop type</th><th>Next hop</th></tr>
<tr><td>Local</td><td>Local</td><td>Local</td></tr>
</tbody> </table>
- Dynamic routing protocols such as BGP and OSPF are not supported.

### Quota Limits

| Resources | Limit |
| :------------------------- | :------ |
| Number of route tables per VPC | 10 |
| Number of route tables associated with each subnet | 1       |
| Number of routing policies per route table | 50 |
