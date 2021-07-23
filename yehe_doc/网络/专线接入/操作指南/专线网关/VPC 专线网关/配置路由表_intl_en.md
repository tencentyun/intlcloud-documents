After creating a direct connect gateway and constructing a dedicated tunnel, you can configure the route table of the VPC in the console to forward the traffic passing through Direct Connect to the direct connect gateway.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Route Tables** on the left sidebar to access the **Route Table** page.
3. Click the **ID/Name** of the route table with which you want to associate the direct connect gateway to go to the details page.
4. Click **+ New routing policies**.
5. In the pop-up window, enter the destination IP range, select **Direct Connect Gateway** for **Next hop type**, and select the specific gateway instance for **Next hop**.
    Configure a routing policy as instructed below.
<table><tbody>
<tr>
<th width="12%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Destination</td>
<td>Specify the destination IP range to which you want to forward traffic. Configure it as follows:
<ul>
<li>Enter an IP range. If you want to enter a single IP, set the mask to 32 (for example, `172.16.1.1/32`).</li>
<li>The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.</li>
</ul>
</td>
</tr>
<tr>
<td>Next hop type</td>
<td>Select <b>Direct Connect Gateway</b>.</td>
</tr>
<tr>
<td>Next hop</td><td>Select the specified direct connect gateway instance to which the traffic is forwarded.</td>
</tr>
<tr>
<tr><td>Notes</td><td>Enter the route description for resource management. This parameter is optional.</td></tr>
</tr>
<tr>
<td>Add a line</td><td>Configure multiple routing policies if needed. You can click the deletion icon in the **Operation** column to delete the unnecessary routing policies. A custom route table should contain at least one routing policy.</td></tr>
</tr>
</tbody> 
</table>
6. Click **Create**.
Now, you can direct the traffic from the specific destination to the direct connect gateway to associate it with your local IDC.

