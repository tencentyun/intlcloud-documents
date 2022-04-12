The EIP using a dedicated BGP IP line reduces the network latency without detouring an international ISP.
>?
>- Currently only bill-by-IP accounts can use the dedicated BGP IPs, and bill-by-CVM accounts need to be upgraded before using these IPs. For details about upgrading, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
>- Dedicated BGP IPs are available only in Hong Kong, China. For details about price, see [Product Pricing](https://intl.cloud.tencent.com/document/product/684/15254).
>- To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Directions
### Step 1. Create a dedicated BGP bandwidth package[](id:step1)
To create an EIP using the dedicated BGP IP line, please create a dedicated BGP bandwidth package first.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** on the left sidebar.
2. At the top of the "Bandwidth Package" page, select the region "Hong Kong (China)", and click **Create** in the upper left corner. 
3. In the "Create Bandwidth Package" window, enter a name, select the "Dedicated BGP" line type and billing mode, and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/12b96572c3f83176697c573f463fa9a9.png" width="53%" />

### Step 2. Create an EIP using the dedicated BGP IP line[](id:step2)
Create an EIP using the dedicated BGP IP line, and add this EIP to the created dedicated BGP bandwidth package.
1. Log in to the [Public IP console](https://console.cloud.tencent.com/cvm/eip).
2. At the top of the "Public IP" page, select the region "Hong Kong (China)", and click **Apply** in the upper left corner.
3. In the pop-up "Apply for EIP" window, configure the following parameters.
<p><img src="https://qcloudimg.tencent-cloud.cn/raw/58569ad0048586eda86140bdcfa6c04b.png" width="50%" /></p>
<table>
<thead>
<tr>
<th width="20%">Parameter</th>
<th width="80%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>IP address type</td>
<td>Select the dedicated BGP IP.
</td>
</tr>
<tr>
<td>Billing mode</td>
<td>Dedicated BGP IPs can be billed by bandwidth package only.
</td>
</tr>
<tr>
<td>Bandwidth package</td>
<td>Select the bandwidth package created in <a href="#step1">Step 1</a>.
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set the bandwidth cap as needed and allocate bandwidth resources reasonably.</td>
</tr>
<tr>
<td>Quantity</td>
<td>Select the quantity of EIPs to be applied as needed and ensure that it does not exceed the total product quota. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/5733?lang=en&pg=#quota-limits">Quota Limit</a>.</td>
</tr>
<tr>
<td><span>Name</span></td>
<td>EIP instance name (optional).</td>
</tr>
<tr>
<td>Tag</td>
<td>You can add a tag and use it for permission management.</td>
</tr>
</tbody></table>



### Step 3. Bind cloud resources
1. Log in to the [Public IP Console](https://console.cloud.tencent.com/cvm/eip), and select the region "Hong Kong (China)".
2. Under the operation column to the right of the target EIP instance, select **More** > **Bind**.
3. In the pop-up "Bind resources" window, select the cloud resource to be bound, and click **OK**.
>?
>- If the bill-by-IP CVM instance already contains a common public IP, release the common public IP first, and then bind it with the EIP.
>- The limit on the number of EIPs bound to CVM instances varies according to the CVM CPUs, as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a>.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/f88b500a296093ed2029968e6f095c53.png" width="60%" />
4. In the pop-up confirmation window, click **OK**.
