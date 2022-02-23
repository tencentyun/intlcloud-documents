## Supported Regions
Lighthouse is currently available in the following regions. We recommend you select the region closest to your target users to reduce the network access latency.
- **Chinese mainland**: Beijing, Guangzhou, Shanghai, Chengdu, and Nanjing.
- **Hong Kong/Macao/Taiwan (China Region)**: Hong Kong (China).
- **Other countries and regions**: Singapore, Silicon Valley, Tokyo, and Moscow.

## Connectivity Description
Both private and public IPs are assigned to Lighthouse instances to provide private and public network connectivity.
* **Private network connectivity**: instances transfer data directly over the local area network (LAN) of Tencent Cloud, thus communicating over the private network for free in the same region. For more information on the use cases and limits, please see [Private network connectivity description](#IntranetUnicom).
* **Public network connectivity**: instances can transfer data over the internet. Tencent Cloud assigns instances public IPs to communicate with other terminals on the internet, enabling them to access and be accessed over the public network. Public network communication consumes instance traffic packages (only outbound traffic is billable in this case).

### Private network connectivity description[](id:IntranetUnicom)
- The table below describes the private network connectivity between Lighthouse instances:
<table>
<tbody><tr>
<th style="width: 36%;">Scenario</th>
<th style=" width: 64%;">Private Network Connectivity Supported by Default</th>
</tr>
<tr>
<td>Interconnection between instances in the same region under the same account    </td>
<td><b>Yes</b>. Please open the corresponding port of the instance firewall. </a>.</td>
</tr>
<tr>
<td>Interconnection between instances in different regions under the same account </td>
<td>No</td>
</tr>
<tr>
<td>Mutual access between instances under different accounts </td>
<td>No</td>
</tr>
</tbody></table>

- The table below describes the private network connectivity between Lighthouse instances and other Tencent Cloud services:
<table>
<tbody>
<tr>
<th style="width: 38%;">Scenario</th>
<th style=" width: 32%;">Private Network Connectivity Supported by Default</th><th style=" width: 30%;">Private Network Connectivity Supported over CCN</th>
</tr>
<tr>
<td>Lighthouse access to CVM</td>
<td>No</td>
<td><b>Yes</b></a>.</td>
</tr>
<tr>
<td>Lighthouse access to COS (in the same region)</td>
<td>
<b>Yes</b>. For more information, please see COS <a href="https://intl.cloud.tencent.com/document/product/436/6224" target="_blank">Regions and Access Endpoints</a>.
<br>You can determine whether Lighthouse accesses COS over the private network by referring to <a href="https://intl.cloud.tencent.com/document/product/1103/41257" target="_blank">FAQs</a>.
</td>
<td>- </td>
</tr>
<tr>
<td>Lighthouse access to COS (in different regions)</td>
<td>No</td>
<td>-</td>
</tr>
<tr>
<td>Lighthouse access to TencentDB</td>
<td>No</td>
<td><b>Yes</b></a>.</td>
</tr>
<tr>
<td>Lighthouse connection to CLB</td>
<td>No</td>
<td>-</td>
</tr>
<tr>
<td>Lighthouse mounting to CFS</td>
<td>No</td>
<td>-</td>
</tr>
</tbody></table>

>!For the above scenarios where private network connectivity is not supported, you can connect over the public network (the outbound traffic of Lighthouse instances will be counted into the traffic packages). In this case, we recommend you take measures such as configuring a reasonable firewall policy to ensure security.
>

### Public network connectivity description
* **Regions in the Chinese mainland**: stable BGP network access is provided to ensure that access to Lighthouse within the Chinese mainland is over a stable low-latency network.
* **Regions outside the Chinese mainland**: the public network bandwidth is mainly provided for users outside the Chinese mainland. Access from the Chinese mainland may experience a significant delay and packet loss due to the ISP network lines (non-cross-border access typically suffers no impact).
>?We recommend you select the region closest to your end users to minimize the access latency and improve the network stability.
>


<style>
.params{margin-bottom:0px !important}
</style>
