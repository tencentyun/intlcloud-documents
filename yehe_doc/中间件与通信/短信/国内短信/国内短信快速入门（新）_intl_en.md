This document uses sending a message `[Tencent Cloud] Your verification code is: XXXX` to mobile numbers in Mainland China as an example to describe how to get started with the Mainland China SMS service. For more concepts related to SMS, please see Common Concepts

>The new version of console is displayed to users who activate the SMS service after September 18, 2019 by default.

## Step 1. Activate the SMS service
### Signing up for a Tencent Cloud account
- If you don't have a Tencent Cloud account yet, you need to [sign up for a Tencent Cloud account and verify your organizational identity.
- If you already have a Tencent Cloud account and verified your identity, you can proceed directly to the next step.

### Applying for activation of SMS
>When logging in to the SMS Console for the first time, you need to apply to activate the SMS service.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2), tick **I have read and agree to Tencent Cloud SMS Service Agreement**, and click **Start Access** to activate the service.
2. Select **Getting Started** on the left sidebar to enter the SMS sending guide page.


## Step 2. Configure SMS content
 A complete SMS message consists of **SMS signature** and **SMS body**. You can set different body templates based on your business needs and then combine a signature and a body into the final SMS content: `[SMS signature] SMS body`. After an SMS signature or template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.


<span id="Sign"></span>
### Creating a signature
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Apply for Mainland China SMS Signature**.
2. Set the following parameters as needed and according to the signature review standards:
 - Signature Type: select **Company**.
 - Signature Purpose: select **For self-use (the signature is a company name, website, product name, or something else verified under the current account)**.
 - Signature Content: enter `Tencent Cloud`.
 - Certificate Type: select **Business license containing unified social credit code**.
 - Certificate Upload: upload a photo or scan of the certificate.
3. Click **OK**.
 Waiting for signature review. The SMS signature will be available only after its status changes to **approved**.

<span id="Template"></span>
### Creating a body template
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Apply for Mainland China SMS Body Template**.
2. Set the following parameters as needed and according to the body template review standards:
 - Template Name: enter `Verification Code`.
 - SMS Type: select **Regular SMS**.
 - SMS content: enter `Your verification code is: {1}`.
3. Click **OK**.
 Waiting for body template review. The body template will be available only after its status changes to **approved**.

## Step 3. Wait for review
After an SMS signature or template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.
On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, you can click [Mainland China SMS Signature Review Status] or [Mainland China SMS Body Review Status] to quickly view the review status. The signature or body template will be available only after its status changes to **approved**.

## Step 4. Send SMS
Before sending an SMS, you need to confirm that both the SMS signature and body template have been approved.
You can send an SMS through the console or API. This article uses the console as an example.

1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Send Mainland China SMS**.
2. Configure the following parameters as needed:
 - Signature Name: select the signature **"Tencent Cloud"** created in the [Creating a signature](#Sign) step.
 - Template Name: select the template **"Verification Code"** created in the [Creating a body template](#Template) step.
 - Delivery Time: select **Send Now**.
 - Recipient: click **Download Standard Template**, enter recipient's mobile number and custom SMS content in the form, and click **Select File** to upload it. The maximum form size supported is 30 MB.
   <table>
     <tr>
         <th width="50%">Recipient's Mobile Number</th>  
         <th>SMS Content Variable 1</th>
		</tr>
	 <tr>      
      <td>Example: 139xxxxxxxx <br>Instructions: please enter the mobile numbers of recipients. All the mobile numbers in one single SMS sending must be registered in Mainland China. The cells need to be in a regular format, i.e., without any specific number formats. </td> 
	     <td>Example: 9097 <br>Instructions: please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>
     </tr> 
</table>


3. Click **OK**.
4. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the status of the task in the Delivery Records list. When the status is **sent**, the task has been completed.

## Step 5. View SMS delivery result
You can view the SMS delivery result in the following ways:
- On the **Mainland China SMS** > **Bulk SMS** page, click **Details & Report Analysis** on the line of the target task to view its detailed record and report analysis.
- Select **Statistics** > **Mainland China SMS** and you can filter and view the statistics and relevant analysis of Mainland China SMS by application, signature, body template, and time.

After the SMS is successfully delivered, the SMS received by the recipient is as shown below: