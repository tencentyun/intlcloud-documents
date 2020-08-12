## Applying in the Console
1. Log in to the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc).
2. Click **+Create** to initiate an application for connection.
You will be required to enter the following information:
<style>
table th:first-of-type {
    width: 150px;
}
</style>

| Parameter | Description | Remarks |
| -------- | ---------------------------------------- | --------------- |
| Direct Connect Name | Name of the connection. | You can change this later. |
| Direct Connect Provider | Available options: China Telecom, China Mobile, China Unicom, and other providers in Mainland China (select this if your direct connect is provided by an ISP in Mainland China other than China Telecom, China Mobile, and China Unicom). If your provider is outside of Mainland China, select Outside Mainland China. | - |
| Access Point | The access point for your Tencent Cloud connection. Select the one near to you. | The city where access points are located usually have at least two access points for dual-line disaster recovery. |
| Cloud Port Type | Specifies the type of the port for bridging the connection with the Tencent Cloud access device. | Select the port type based on your bandwidth. You can consult with your Direct Connect provider or Tencent Cloud's architect or after-sales manager. |
| Your IDC Location | Detailed address. | The floor of the IDC should be provided in the detailed address. |
| Bandwidth | 2 - 100,000 Mbps | - |
| Carrier Circuit ID | The unique circuit ID provided by the direct connect provider for line identification and protection. | 
| Redundant Connection | Use a second access device for the redundant connection instead of having both connections plugged in to the same device. That way, he first access device and the second one can form a mast/slave configuration to avoid single point of failure. | The purpose of setting master/slave connections is to avoid two lines connecting to the same access point. The master/slave relation of dedicated tunnels must be applied for on the dedicated tunnel product page. |
| Applicant Name | The name of the contact person for Direct Connect. | - |
| Applicant Mobile Number | The mobile number of the contact person for Direct Connect. | - |
| Applicant Email | The email address of the contact person for Direct Connect. | - |

After the application is submitted, the status of the connection will become **Applying**. A Tencent Cloud Direct Connect representative will evaluate your application within 3 business days.

## Resource Review and Confirmation
- After your application is submitted, Tencent Cloud’s Direct Connect representative will conduct a comprehensive assessment of Direct Connect resources and then discuss service details with you over the phone. Once it is confirmed that Direct Connect can be connected, your Direct Connect status will become "Pending Payment".
- Your Direct Connect application may be rejected for one of the following reasons:
 - Inaccurate information: the access information you entered is incomplete. Please update the information according to the feedback of the Direct Connect representative and submit a new application.
 - Insufficient resources: the access port or uplink bandwidth resources are insufficient. Please submit a new application according to the Direct Connect representative’s feedback after the resources are available.
 - Disqualification: the connection is only available to large-scale enterprise customers. Please submit a new application after updating your enterprise qualification.

## Payment and Acceptance
You can make the payment once your application is approved.
1. Log in to the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc).
2. Find the desired connection in the connection list, and click **Pay Now**.
3. Confirm the Direct Connect information in the page that appears, and click **OK**.
4. Enter the billing platform to complete the payment.

After your payment is made, your Direct Connect representative will accept the access request and assist you with connection setup by coordinating various resources. After the setup is complete, the status of your Direct Connect will change to "Running".
