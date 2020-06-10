This document uses sending a message `Your verification code is 1234 (valid for 5 minutes). For account safety, don't forward the code to others.` to mobile numbers outside Mainland China as an example to describe how to get started with the Global SMS service. For more concepts related to SMS, please see [Common Concepts](https://intl.cloud.tencent.com/document/product/382/13299).

>The new version of console is displayed to users who activate the SMS service after September 18, 2019 by default.

## Step 1. Activate the SMS service
### Signing up for a Tencent Cloud account
- If you don't have a Tencent Cloud account yet, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your organizational identity.
- If you already have a Tencent Cloud account and verified your identity, you can proceed directly to the next step.

### Applying for activation of SMS
>When logging in to the SMS Console for the first time, you need to apply to activate the SMS service.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2), tick **I have read and agree to Tencent Cloud SMS Service Agreement**, and click **Start Access** to activate the service.
2. Select **Getting Started** on the left sidebar, select **Send Global SMS**, and click **Start** to enter the SMS sending guide page.

## Step 2. Configure SMS content
 A complete SMS message consists of **SMS signature** and **SMS body**. You can set different body templates based on your business needs and then combine a signature and a body into the final SMS content: `[SMS signature] SMS body`. After an SMS signature or template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.
Signature is optional for Global SMS. This document uses no signature as an example.

<span id="Template"></span>
### Creating a body template
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Create**.
2. Set the following parameters as needed:
 - Template Name: enter `Verification Code`.
 - SMS Type: select **Regular SMS**.
 - SMS Content: enter `Your verification code is {1} (valid for {2} minutes). For account safety, don't forward the code to others.`.
3. Click **OK**.
 Waiting for body template review. The body template will be available only after its status changes to **approved**.

## Step 3. Wait for review
After an SMS signature or body template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.
On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, you can click **View** to quickly view the review status. The signature or body template will be available only after its status changes to **approved**.

## Step 5. Send SMS
Before sending an SMS, you need to confirm that both the SMS signature and body template have been approved.
You can send an SMS through the console or [API](https://intl.cloud.tencent.com/document/product/382/34689). This document uses the console as an example.

1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Send SMS**.
2. Configure the following parameters as needed:
 - Signature Name: signature is optional for Global SMS.
 - Template Name: select the template **"Verification Code"** created in the [Creating a body template](#Template) step.
 - Delivery Time: select **Send Now**.
 - Recipient: click **Template Download**, enter recipient's mobile number and custom SMS content in the form, and click **Select File** to upload it. The maximum form size supported is 30 MB.
   <table>
     <tr>
         <th width="30%">Recipient's Mobile Number</th>  
         <th width="35%">SMS Content Variable 1</th>  
         <th width="35%">SMS Content Variable 2</th>
		</tr>
	 <tr>      
      <td>Example: 9xxxxxxx <br>Instructions: please enter the mobile numbers of recipients. All the mobile numbers in one single SMS sending must be registered outside Mainland China. The cells need to be in a regular format, i.e., without any specific number formats. </td>   
	     <td>Example: 1234 <br>Instructions: please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>   
	     <td>Example: 5 <br>Instructions: please enter the second custom variable content according to the body template, i.e., replacing {2} in the template. </td>
     </tr> 
</table>
4. Click **OK**.
5. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the status of the task in the Delivery Records list. When the status is **sent**, the task has been completed.

## Step 5. View SMS delivery result
You can view the SMS delivery result in the following ways:
- On the **Global SMS** > **Bulk SMS** page, click **Details & Report Analysis** on the line of the target task to view its detailed record and report analysis.
- Select **Statistics** > **Global SMS** and you can filter and view the statistics and relevant analysis of Global SMS by application, signature, body template, and time.


