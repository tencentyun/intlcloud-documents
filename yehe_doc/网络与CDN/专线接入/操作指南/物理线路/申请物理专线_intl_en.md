All connection access applications (including BM and ECN) need to be initiated and completed in the console. Tencent Cloud Direct Connect is only available to certified Tencent Cloud organizational customers.
Follow the instructions below to apply for and set up a Tencent Cloud connection.

## Applying in the Console
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Click **+New** to initiate an application for connection.
You will be required to enter the following information:
<style>
table th:first-of-type {
    width: 150px;
}
</style>

| Parameter | Description | Remarks |
| -------- | ---------------------------------------- | --------------- |
| Connection Name | Enter a name for your connection. | You can change this later. |
| Connection Provider | Select from the following options: CTCC, CMCC, CUCC, other Chinese mainland carriers (for a connection provided by carriers in the Chinese mainland rather than the three listed out), and outside the Chinese mainland (for a connection provided by carriers outside the Chinese mainland). | - |
| Access Location | The access point for your Tencent Cloud connection. Nearby access is recommended. | Generally, two or more access points are available in one Tencent Cloud region, implementing two-connection disaster recovery. |
| Cloud port type | The port used to connect your connection with the Tencent Cloud access device | Select the port type based on your bandwidth. You can consult with your connection provider or Tencent Cloud's architect or after-sales manager. |
| Your Premise | Enter your detailed address. | The floor of the IDC should be provided in the detailed address. |
| Bandwidth Cap      | <ul><li>Set a bandwidth cap between 1-1,000 Mbps for a GbE port.</li><li>Set a bandwidth cap between 1-10,000 Mbps for a 10 GbE port.</li></ul>      |      -           |
| Carrier Circuit ID | The unique circuit ID of this connection provided by the carrier | - |
| Redundant Connection | A second connection for the primary/secondary configuration, instead of having both connections connecting to the same device. This avoids single points of failure. | The primary/secondary configuration is to avoid two connections connecting to the same access point. To configure primary and secondary dedicated tunnels, you need to apply for them on the Dedicated Tunnels console.|
| Applicant Name | The name of the contact person for Direct Connect | - |
| Applicant Mobile | The mobile number of the contact person for Direct Connect | - |
| Applicant Email | The email address of the contact person for Direct Connect | - |


## Reviewing Resources and Designing Solutions[](id:buzhou2)
After your application for a connection is submitted, Tencent Cloud’s Direct Connect representative will comprehensively assess Direct Connect resources and then check with you the service details over the phone. After the connection is confirmed to be accessible, its status becomes **Pending paid**. Your connection application may be rejected for any of the following reasons:
- Inaccurate information: the access information you entered is incomplete. Please modify your application according to the feedback of the Direct Connect representative, and submit again.
- Insufficient resources: the access port or uplink bandwidth resources are insufficient. Please submit a new application after the Direct Connect representative confirms the resource availability.
- Ineligibility: the connection is only available to large-scale organizational customers. After you are eligible, resubmit an application.


## Completing the Payment[](id:buzhou3)
After your application is approved, you need to complete the payment on the console. Then the Direct Connect representative will accept the access request and coordinate resources for the connection construction. After the connection is completed and accepted, the connection status becomes **Running**. Perform the following steps to make the payment:

1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc).
2. Locate the connection to be paid for in the connection list, and click **Pay Now**.
3. Confirm the Direct Connect information in the pop-up window, and click **OK**.
4. Access the billing platform to complete the payment.

## Configuring Alarm Recipient
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
<td>1 minute</td>
<td>>=</td>
<td>80%</td>
<td>At 5 consecutive data points</td>
<td>Alarm once a day</td>
</tr>
</table>

This default alarm policy is not provided with a recipient, so you can only view alarms in the console Message Center. To configure a recipient, perform the following steps.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and choose **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. Click **Advanced Filter** in the top-right corner of the **Alarm Policy** page, select **All** for the **Monitor Type** and **Physical dedicated line** for the **Policy type**.
3. Perform the following operations as needed.
 - Configure alarm objects
      1. Click the name of the target default policy in the “Alarm Policy” list.
      2. Select a template in the **Alarm Notification** section, and configure recipients in the template. If existing templates are not suitable, you can click **Create Template** and configure it as prompted.
 - Modify an alarm policy
      1. Click the name of the target default policy in the “Alarm Policy” list.
      2. Click **Edit** next to the **Trigger Condition** and modify the trigger conditions for metric alarms and event alarms in the pop-up window. For more information on alarms, please see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403). After the modification is complete, click **Save**.
 - Set a default policy
      If the default alarm policy cannot meet your needs, you can select a custom alarm policy and click **Set to Default Policy** in the **Operation** column. Then the selected alarm policy will automatically apply to connections created afterwards.

## Subsequent Operations

After the carrier completes the connection construction, you need to test and accept it by creating a direct connect gateway and a dedicated tunnel. The accepted connection will be in **Running** status.
- [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256)
- [Creating a Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/19250)
- [Configuring a Route Table](https://intl.cloud.tencent.com/document/product/216/19259)
