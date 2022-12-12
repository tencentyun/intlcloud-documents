This document introduces how to create a connection in the Tencent Cloud console.

## Process
![](https://qcloudimg.tencent-cloud.cn/raw/9308b979285e8de12b92cbb31e8701ed.jpg)
>?After creating a connection, contact your Tencent Cloud sales rep promptly to further configure it. If you don't have a sales rep, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>
1. [Create a connection](#buzhou1): Synchronize your connection application in the console. Then, the connection status will become **Applying**.
2. [Review resources and design solutions](#buzhou2): Tencent Cloud will review resources after receiving your connection application. The connection status becomes **Evaluating**. Then, the connection manager will confirm the connection design with you synchronously. After confirmation, the connection status turns to be **Pending paid**.
3. [Complete the payment](#buzhou3): After the payment is completed in the console, the connection status will be changed to **Constructing**. You also need to contact the carrier and Tencent Cloud to complete the connection construction and acceptance, and confirm the acceptance in the console. The accepted connection will be in **Running** status.
>?From February 1, 2021, Tencent Cloud permanently reduces or exempts the initial installation fee for all newly created connections. During the application process, the connection status will be directly transferred from **Evaluating** to **Constructing**, with **Pending paid** status being cancelled.
> 

## Directions
### Step 1. Create a connection[](id:buzhou1)
After the application is submitted, the connection status will become **Applying**. Tencent Cloud will assess resources and provide solutions within three business days.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **+New** on the **Connections** page.
2. Complete the following configurations and click **OK**.
![]()
<table>
<tr>
<th width="15%">Parameter</th>
<th width="45%">Description</th>
<th width="40%">Remarks</th>
</tr>
<tr>
<td>Connection name</td>
<td>Set a name for your connection.</td>
<td>You can rename your connection.</td>
</tr>
<tr>
<td>Region</td>
<td>Select the geographic area of a physical data center. Tencent Cloud regions are completely isolated from each other to ensure maximum stability and fault tolerance between different regions.</td>
<td>To reduce the access delay and improve the download speed, we recommend you choose the nearest region.</td>
</tr>
<tr>
<td>Access point</td>
<td>Select the network service provider of Tencent Cloud connection. We recommend you choose the nearest access point. For details, see <a href="https://intl.cloud.tencent.com/document/product/216/41429"> Connection Access Point</a>.</td>
<td>A region supported by Tencent Cloud generally has more than two access points, which can realize two-line disaster recovery.</td>
</tr>
 <tr>
<td>Connection provider</td>
<td>Select a carrier with compliant telecommunication business operation qualifications.</td>
<td>CTCC, CMCC, CUCC, local connection carriers, other carriers in/outside the Chinese mainland.</td>
</tr>
<tr>
<td>Cloud port</td>
<td>Supported specifications: 1G, 10G and 100G.</td>
<td>To use 100G ports, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr>
<tr>
<td>Port type</td>
<td>Choose fiber optic port or electrical port as needed. The available ports vary with the port type. For example, 1G ports include fiber optic port and electrical port, while 10G ports only include fiber optic port.</td>
<td>Select the appropriate interface based on your bandwidth. For technical support, consult your connection service provider or Tencent Cloud architect/after-sales manager.</td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td><ul><li>Set a bandwidth cap between 1-1,000 Mbps for a 1G port.</li><li>Set a bandwidth cap between 1-10,000 Mbps for a 10G port.</li></ul></td>
<td>- </td>
</tr>
<tr>
<td>IDC address</td>
<td>Select the specific address of the user IDC.</td>
<td>- </td>
</tr>
<tr>
<td>Contact person</td>
<td>Enter the name of customer-side contact person for applying for a connection.</td>
<td>For example, John Smith.</td>
</tr>
<tr>
<td>Contact details</td>
<td>Enter the contact details of customer-side contact person for applying for a connection.</td>
<td>- </td>
</tr>
<tr>
<td>Applicant email</td>
<td>Enter the email address of the connection applicant.</td>
<td>XXXX@XXXX.com.</td>
</tr>
</table>

### Step 2. Review resources and design solutions[](id:buzhou2)
After your application for a connection is submitted, Tencent Cloud's Direct Connect representative will comprehensively assess Direct Connect resources and then check with you the service details over the phone. After the connection is confirmed to be accessible, its status becomes **Pending paid**. Your connection application may be rejected for any of the following reasons:
- Inaccurate information: The access information you entered is incomplete. Modify your application according to the feedback of the Direct Connect representative, and submit again.
- Insufficient resources: The access port or uplink bandwidth resources are insufficient. Submit a new application after the Direct Connect representative confirms the resource availability.
- Ineligibility: The connection is only available to large-scale organizational customers. After you are eligible, resubmit an application.


### Step 3. Complete the payment[](id:buzhou3)
After your application is approved, you need to complete the payment on the console. Then the Direct Connect representative will accept the access request and coordinate resources for the connection construction. After the connection is completed and accepted, the connection status becomes **Running**. Perform the following steps to make the payment:

1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Locate the connection to be paid for in the connection list, and click **Pay Now**.
3. Confirm the Direct Connect information in the pop-up window, and click **OK**.
4. Access the billing platform to complete the payment.

### Step 4. Configure the alarm recipient
After a connection is created, Tencent Cloud automatically configures the following metric alarm for its bandwidth utilization, helping you monitor and manage your connection.
<table>
<tr>
<th>Metric</th>
<th>Statistical Period</th>
<th>Condition</th>
<th>Threshold</th>
<th>Duration</th>
<th>Policy</th>
</tr>
<tr>
<td>dc_band_rate</td>
<td>One minute</td>
<td>>=</td>
<td>80%</td>
<td>At five consecutive data points</td>
<td>Alarm once a day</td>
</tr>
</table>

The automatically created default alarm policy is not configured with recipient information, and only supports console alarms. You can configure alarm recipients by yourself. For details, see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/216/38402).

## Subsequent Operations
After the carrier completes the connection construction, you need to test and accept it by creating a direct connect gateway and a dedicated tunnel. The accepted connection will be in **Running** status.
- [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256)
- [Creating a Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/19250)
- [Configuring a Route Table](https://intl.cloud.tencent.com/document/product/216/19259)
