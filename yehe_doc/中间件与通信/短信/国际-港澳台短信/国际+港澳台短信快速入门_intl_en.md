This document uses sending a message `Your verification code is 1234 (valid for 5 minutes). For account safety, don't forward the code to others.` to mobile numbers outside Mainland China as an example to describe how to get started with the Global SMS service. For more concepts related to SMS, please see [Common Concepts](https://intl.cloud.tencent.com/document/product/382/13299).

>?The new version of console is displayed to users who activate the SMS service after September 18, 2019 by default.

## Step 1. Activate the SMS service
### Signing up for Tencent Cloud account
- If you don't have a Tencent Cloud account yet, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verify your organizational identity](https://intl.cloud.tencent.com/document/product/378/10496).
- If you already have a Tencent Cloud account and verified your identity, you can proceed directly to the next step.

### Applying for activation of SMS
>?When logging in to the SMS console for the first time, you need to apply to activate the SMS service.

1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2), click **I've read and agree to Tencent Cloud SMS Service Agreement**, and click **Start Access** to activate the service.
2. Select **Getting Started** on the left sidebar, select **I want to send Global SMS**, and click **Start** to enter the SMS sending guide page.
 

## Step 2. Configure SMS content
 A complete SMS message consists of **SMS signature** and **SMS body**. You can set different body templates based on your business needs and then combine a signature and a body into the final SMS content: `[SMS signature] SMS body`. After an SMS signature or template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.
Signature is optional for Global SMS. This document uses no signature as an example.

[](id:Template) 
### Creating body template
1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Create**.
2. Set the following parameters as needed and according to the [body template review standards](https://intl.cloud.tencent.com/document/product/382/40659):
 - Template Name: enter `Verification Code`.
 - SMS Type: select **Regular SMS**.
 - SMS Content: enter `Your verification code is {1} (valid for {2} minutes). For account safety, don't forward the code to others.`.
3. Click **OK**.
 Waiting for body template review. The body template will be available only after its status changes to **approved**.

## Step 3. Wait for approval
After an SMS signature or body template is submitted, it will be reviewed within two hours generally. You can set your mobile number and email address to receive review result notifications.
On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, you can click **View** to quickly view the review status. The signature or body template will be available only after its status changes to **approved**.

## Step 4. Send SMS messages
Before sending an SMS message, you need to confirm that both the SMS signature and body template have been approved.
You can send an SMS through the console or [API](https://intl.cloud.tencent.com/document/product/382/40463). This document uses the console as an example.

1. On the [Getting Started](https://console.cloud.tencent.com/smsv2/guide) page, click **Send SMS**.
 
2. Configure the following parameters as needed:
 - Signature Name: signature is optional for Global SMS.
 - Template Name: select the template **"Verification Code"** created in the [Creating a body template](#Template) step.
 - Delivery Time: select **Send Now**.
 - Recipient: select **Upload mobile numbers**, click **Download Standard Template**, enter the recipient's mobile number and custom SMS content in the form, and click **Click here** to upload it. The maximum form size supported is 30 MB.
 <table>
     <tr>
				 <th width="1%">Template Description</th>
         <th width="35%">Recipient's Mobile Number</th>  
         <th width="15%">SMS Content Variable 1</th>
				 <th width="15%">SMS Content Variable 2</th>
		</tr>
	 <tr>
		 <td>Sample</td>
      <td>9xxxxxxx</td> 
	    <td>1234</td>
			<td>5</td>
     </tr> 
		 <td>Instructions</td>
      <td>Please enter the mobile numbers of recipients. All the mobile numbers in one single SMS delivery task must be registered outside Mainland China. The cells need to be in a regular format, i.e., without any specific number formats. </td> 
	     <td>Please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>
			 <td>Please enter the first custom variable content according to the body template, i.e., replacing {2} in the template. </td>
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
      <td><ul><li>You can upload up to 1 million mobile numbers in a CSV or XLSX file of up to 30 MB in size for each bulk SMS delivery task. </li><li>In an SMS body template created by an individual user, each variable can contain up to 12 characters. <li>There is no limit on the length of variable values for organizational users.</li></ul></td> 
	     <td>Supported</td>
     </tr>
		 <tr>
		 <td>Select a customer group</td>
      <td>Click **Customer Group** and select a number group that has been created in <a href = "https://console.cloud.tencent.com/smsv2/phone-manage/group-manage">Customer Group</a>. For more information, please see <a href = "https://cloud.tencent.com/document/product/382/48787">Customer Management</a>. <br><b>Note:</b> you cannot select a template with variables for <a href = "#model">Template Name</a>.</td> 
	     <td>Not supported</td>
     </tr> 		
		 		 <tr>
		 <td>Enter mobile numbers</td>
      <td>Enter up to 100 mobile numbers and separate them by pressing the Enter key (one number per line).
For mobile numbers outside Mainland China, please enter the country/region code + mobile number. <br>For example, when the country/region code is 852 and the mobile number is 6666XXXX, enter 8526666XXXX. <br><b>Note:</b> you cannot select a template with variables for <a href = "#model">Template Name</a>. </td> 
	     <td>Not supported</td>
     </tr> 
</table>
 - Application: select the application that needs to send the SMS. For more information, please see [Creating Application](https://intl.cloud.tencent.com/document/product/382/35468). 
3. Click **OK**.
4. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the status of the task in the Delivery Records list. When the status is **Sent**, the task has been completed.

## Step 5. View SMS delivery result
You can view the SMS delivery result in the following ways:
- On the **Global SMS** > **Bulk SMS** page, click **Details & Receipt Analytics** on the line of the target task to view its detailed record and report analysis.
- Select **Statistics** > **Global SMS** and you can filter and view the statistics and relevant analysis of Global SMS by application, signature, body template, and time.
