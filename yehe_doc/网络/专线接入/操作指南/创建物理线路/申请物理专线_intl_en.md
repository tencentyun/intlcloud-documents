All connection access applications (including BM and ECN) need to be initiated and completed in the console. Tencent Cloud Direct Connect is only available to certified Tencent Cloud enterprise customers.
Follow the instructions below to apply for and set up a Tencent Cloud connection.

## Applying in the Console
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Click **New** to initiate an application for connection.
You will be required to enter the following information:
<style>
table th:first-of-type {
    width: 150px;
}
</style>

| Parameter | Description | Remarks |
| -------- | ---------------------------------------- | --------------- |
| Connection Name | Enter a name for your connection | You can change this later |
| Connection Provider | Select from the following options: CTCC, CMCC, CUCC, other Chinese mainland carriers (for a connection provided by all carriers in the Chinese mainland other than the aforementioned three carriers), and outside the Chinese mainland (for a connection provided by carriers outside the Chinese mainland) | - |
| Access Location | The access point for your Tencent Cloud connection. Nearby access is recommended | Generally, two or more access points are available in one Tencent Cloud region, enabling two-connection disaster recovery |
| Cloud Port Type | The port used to connect your connection with the Tencent Cloud access device | Select the port type based on your bandwidth. You can consult with your connection provider or Tencent Cloud's architect or after-sales manager |
| Your IDC Location | Detailed address | The floor of the IDC should be provided in the detailed address |
| Bandwidth | Valid range: 2 - 100,000 Mbps | - |
| Carrier Circuit ID | The unique circuit ID of this connection provided by the carrier | - |
| Redundant Connection | A second connection for the primary/secondary configuration instead of having both connections connect to the same device, avoiding single points of failure | The primary/secondary configuration is to avoid two connections connecting to the same access point. To configure primary and secondary dedicated tunnels, you need to apply for them on the Dedicated Tunnels console |
| Applicant Name | The name of the contact person for Direct Connect | - |
| Applicant Mobile | The mobile number of the contact person for Direct Connect | - |
| Applicant Email | The email address of the contact person for Direct Connect. | - |


## Resource Review and Confirmation
After your application is submitted, Tencent Cloud’s Direct Connect representative will comprehensively assess Direct Connect resources, which changes the connection status to **Evaluating**. Then the representative will check the service details with you over the phone. After the connection is confirmed to be accessible, its status will become **Pending payment**.
Your connection application may be rejected for any of the following reasons:

- Inaccurate information: the access information you entered is incomplete. Please modify your application according to the feedback of the Direct Connect representative, and submit it again.
- Insufficient resources: the access port or uplink bandwidth resources are insufficient. Please submit a new application after the Direct Connect representative confirms the resource availability.
- Ineligibility: the connection is only available to large-scale enterprise customers. After you become eligible, resubmit an application.

## Payment
After your application is approved, you need to complete the payment on the console. Then your Direct Connect representative will accept the access request and coordinate resources for the connection setup. After the setup is completed, the connection status will become **Running**. Perform the following steps to make the payment.

You can make a payment once your application is approved.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Locate the connection to be paid for in the connection list, and click **Pay Now**.
3. Confirm the Direct Connect information in the pop-up window, and click **OK**.
4. Access the billing platform to complete the payment.

## Default Alarm
After a connection is created, Tencent Cloud will automatically configure the following metric alarm for the connection’s bandwidth utilization, helping you monitor and manage your connection.
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
<td>1 minute</td>
<td>>=</td>
<td>80%</td>
<td>Continuous 5 periods</td>
<td>Alarms every day</td>
</tr>
</table>

This default alarm policy is not provided with a recipient, so you can only view alarms in the console Message Center. To configure a recipient, perform the following steps.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. On the **Alarm Policy** page, click **Advanced Filter** and select **Direct Connect** for **Policy Type**.
3. Perform the following operations as needed.
 - Configure alarm recipient objects
     1. Click the name of the target default policy in the alarm policy list.
     2. Click **Edit** next to **Alarm Object** and select the object from the list in the pop-up window. You can also click **Add Object** to configure new alarm objects.
 - Modify an alarm policy
     1. Click the name of the target default policy in the alarm policy list.
     2. Click **Edit** next to **Alarm Rule** and modify the trigger conditions in the pop-up window. For more information on alarm rules, please see the “Metric Alarms” section in [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403). After completing the modification, click **Save**.
 - Set a default policy
     If the default alarm policy cannot meet your needs, you can select a custom alarm policy and click **Set to Default Policy** under the **Operations** column. Then the selected alarm policy will automatically apply to connections that are created afterwards.

## Subsequent Operations

After the carrier completes the connection setup, you need to create a direct connect gateway and dedicated tunnel as instructed below to perform the connection acceptance. The accepted connection will be in **Running** status.
- [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256)
- [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250)
- [Configuring the Route Table](https://intl.cloud.tencent.com/document/product/216/19259)