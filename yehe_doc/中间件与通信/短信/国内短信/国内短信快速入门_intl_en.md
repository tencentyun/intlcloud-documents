This document helps you quickly get started with the Chinese mainland SMS service by show you how an organization user sends the following message `[Tencent Cloud] Your verification code is: XXXX` to mobile numbers in the Chinese mainland. For more SMS concepts, see [Glossary](https://intl.cloud.tencent.com/document/product/382/13299).

>?The new version of console is displayed to users who activate the SMS service after September 18, 2019 by default.

## Step 1: Activate the SMS service
### Signing up for Tencent Cloud account
- If you don't have a Tencent Cloud account yet, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verify your organizational identity](https://intl.cloud.tencent.com/document/product/378/10496).
- If you already have a Tencent Cloud account and have verified your identity, go directly to the next step.

### Applying for activation of SMS
>?When logging in to the SMS console for the first time, you need to apply to activate the SMS service.

1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2), click **I've read and agree to Tencent Cloud SMS Terms of Service**, and click **Access** to activate the service.
2. Select **Getting Started** on the left sidebar and click **Start creating** to enter the SMS sending guide page.

## Step 2. Configure SMS content
 A complete SMS message consists of **SMS signature** and **SMS body**. You can set different body templates as needed and then combine a signature and a body into the final SMS content: `[SMS signature] SMS body`. After an SMS signature or template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.

### Selecting a region
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, select a region in the top-left corner.
Tencent Cloud International offers services in many regions with the same product features and prices. However, data cannot be stored across regions and must instead be kept in the local region. Please select a region based on your data storage needs.
![](https://qcloudimg.tencent-cloud.cn/raw/ec3a87b4037656c52d735f4d98f77b24.png)

[](id:Sign)
### Creating a signature
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Start creating**.
2. Set the following parameters as needed:
 - Signature Purpose: select **For verified entities (such as organizations, websites or product names with signatures verified by the account)**.
 - Signature Type: select **Company**.
 - Signature Content: enter `Tencent Cloud`.
 - Certificate Type: select **Three-in-one**.
 - Certificate Upload: upload a photo or scan of the certificate.
3. Click **OK**.
 Please wait for the signature review. The signature will be available only after its status changes to **Approved**.

[](id:Template)
### Creating a body template
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Start creating**.
2. Set the following parameters as needed:
 - Template Name: enter `Verification Code`.
 - SMS Type: select **Regular SMS**.
 - SMS content: enter `Your verification code is: {1}`.
3. Click **OK**.
 Please wait for the body template review. The body template will be available only after its status changes to **Approved**.

## Step 3. Wait for approval
After an SMS signature or body template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.
On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, you can click **View** to quickly view the review status of the signature or body template. The signature or body template will be available only after its status changes to **approved**.

## Step 4. Send SMS messages
>!
>1. SMS signatures and templates for each region need to be separately created, but they can be copied across regions. Before sending an SMS message, make sure the region selected for the SMS application is the same as that selected for signature and template creation.
>2. Before sending an SMS message, make sure the SMS signature and body template have been approved.  

You can send SMS messages through the console or [API](https://intl.cloud.tencent.com/document/product/382/40463). This document uses the console as an example.

1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Send SMS**.
2. Configure the following parameters as needed:
 - Signature Name: select the signature **"Tencent Cloud"** created in the [Creating a signature](#Sign) step.
 - Template Name: select the template **Verification Code** created in the [Creating a body template](#Template) step.[](id:model)
 - Sending Time: select **Send now**.
 - Recipient: select **Upload mobile numbers**, click **Download Standard Template**, enter the recipient's mobile number and custom SMS content in the form, and click **Click here** to upload it. The maximum form size supported is 30 MB.
<table>
     <tr>
				 <th>Template Description</th>
         <th width="50%">Recipient's Mobile Number</th>  
         <th>SMS Content Variable 1</th>
		</tr>
	 <tr>
		 <td>Sample</td>
      <td>139xxxxxxxx</td> 
	     <td>9097</td>
     </tr> 
		 <td>Instructions</td>
      <td>Please enter the mobile numbers of recipients. All the mobile numbers in one single SMS sending task must be registered in the Chinese mainland. The cells need to be in a regular format, i.e., without any specific number formats.</td> 
	     <td>Please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>
     </tr>
</table>
<b>There are three types of recipients as follows: </b><span id = "object"></span>
<table>
     <tr>
				 <th>Recipient</th>
         <th>Description</th>  
         <th>Variable Template</th>
		</tr>
	 <tr>
		 <td>Upload mobile numbers</td>
      <td><ul><li>You can upload up to 1 million mobile numbers in a CSV or XLSX file of up to 30 MB in size for each bulk SMS sending task. </li><li>In an SMS body template created by an individual user, each variable can contain up to 12 characters. <li>There is no limit on the length of variable values for organizational users.</li></ul></td> 
	     <td>Supported</td>
     </tr>
		 <tr>
		 <td>Select a customer group</td>
      <td>Click **Customer Group** and select a number group that has been created in <a href = "https://console.cloud.tencent.com/smsv2/phone-manage/group-manage">Customer Group</a>. <br><b>Note:</b> you cannot select a template with variables for <a href = "#model">Template Name</a>.</td> 
	     <td>Not supported</td>
     </tr> 		
		 		 <tr>
		 <td>Enter mobile numbers</td>
      <td>Enter up to 100 mobile numbers and separate them by pressing the Enter key (one number per line).
For the Chinese mainland mobile numbers, please enter the mobile numbers directly: <br>For example, 1371481xxxx. <br><b>Note:</b> you cannot select a template with variables for <a href = "#model">Template Name</a>.</td> 
	     <td>Not supported</td>
     </tr> 
</table>
 - Application: select the application that needs to send the SMS. For more information, please see [Creating Application](https://intl.cloud.tencent.com/document/product/382/35468).
3. Click **OK**.
4. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the task status in the “Sending Records” list. The status **Sent** indicates the task has been completed.

## Step 5. View SMS delivery result
You can view the SMS delivery result in the following ways:
- On the **Chinese Mainland SMS** > **Bulk SMS** page, click **Details & Receipt Analytics** on the line of the target task to view its detailed record and receipt analysis.
- Select **Statistics** > **Chinese Mainland SMS** and you can filter and view the statistics and relevant analysis of Chinese Mainland SMS by application, signature, body template, and time.


