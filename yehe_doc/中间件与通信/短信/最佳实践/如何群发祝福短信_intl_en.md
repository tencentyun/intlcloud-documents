
Best wishes for birthdays, holidays, and other matters is an important way for enterprises to retain existing customers. You can use Tencent Cloud SMS to send such messages to users on special days such as holidays, member birthdays (anniversaries), and days of major weather changes for customer care.
>?Best wishes messages are marketing SMS and can be sent only by **verified organizational users**. For more information, please see [Differences in Rights](https://intl.cloud.tencent.com/document/product/382/13444#.E6.9D.83.E7.9B.8A.E5.8C.BA.E5.88.AB).

This document uses sending a Spring Festival best wishes message to members by company A as an example to describe how to send such messages quickly.

## Preparations
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your organizational identity.
- [Purchase](https://intl.cloud.tencent.com/document/product/382/35450) an SMS package.
- Prepare SMS signature owner qualification certificates.
 This document takes a business license as a qualification certificate for example.
- Understand the SMS body content review standards.


<span id="Step1"></span>
## Step 1. Create a signature

>?After an SMS signature is submitted, it will be reviewed within two hours generally. You can [configure alarm contacts](https://intl.cloud.tencent.com/document/product/382/35470) to receive review result notifications.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Chinese Mainland SMS** > **Signatures** on the left sidebar and click **Create Signature**.
3. Set the following parameters as needed and according to the signature review standards:
 <table>
     <tr>
         <th>Parameter</th>  
         <th nowrap="nowrap">Sample Value</th>  
     </tr>
	 <tr>      
       <td>Signature use</td>   
	     <td>For verified entities (such as organizations, websites or product names with signatures verified by the account)</td>   
     </tr> 
	 <tr>      
       <td>Signature type</td>   
	     <td>Company</td>   
     </tr> 
	 <tr>      
       <td>Signature content</td>   
	     <td>A Co., Ltd.</td>   
     </tr> 
	 <tr>      
       <td>Certificate type</td>   
	     <td>	Business license</td>   
     </tr> 
	 <tr>      
       <td>Certificate upload</td>   
	<td><img src="https://main.qcloudimg.com/raw/d7547d5ca6c257be994112409cf88a53.jpg" width=200/></td>     
     </tr> 
</table>
3. Click **OK**.
 Wait for signature review. The SMS signature will be available only after its status changes to **approved**.

<span id="Step2"></span>
## Step 2. Create a body template
>After an SMS body template is submitted, it will be reviewed within two hours generally. You can [configure alarm contacts](https://intl.cloud.tencent.com/document/product/382/35470) to receive review result notifications.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Chinese Mainland SMS** > **Body Templates** on the left sidebar and click **Create Body Template**.
3. Set the following parameters as needed and according to the body template review standards:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th nowrap="nowrap">Sample Value</th>  
     </tr>
	 <tr>      
        <td>Template name</td>   
	     <td>Best wishes message</td>   
     </tr> 
	 <tr>      
        <td>SMS type</td>   
	     <td>Marketing SMS</td>   
     </tr> 
	 <tr>      
        <td>SMS content</td>   
	     <td>Dear Ms./Mr. {1}, thank you for your always support and trust. We want to extend our Spring Festival greetings and best wishes to you and your beloved ones.</td>   
     </tr> 
</table>
4. Click **OK**.
 Wait for body template review. The body template will be available only after its status changes to **approved**.


<span id="Step3"></span>
## Step 3. Send SMS
Before sending an SMS, you need to confirm that both the SMS signature and body template have been approved.
You can send an SMS through the console or [API](https://intl.cloud.tencent.com/document/product/382/34859). This document uses the console as an example.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Chinese Mainland SMS** > **Bulk SMS** on the left sidebar and click **Create Bulk SMS Sending Task**.
3. Configure the following parameters as needed:
 <table>
     <tr>
         <th nowrap="nowrap">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>
	     <td>Signature name</td>   
	     <td>Select the signature [A Co., Ltd.] created in <a href="#Step1">step 1</a></td>   
     </tr> 
	 <tr>
	     <td>Template name</td>   
	     <td>Select the **Best wishes message** created in <a href="#Step2">step 2</a></td>   
     </tr> 
	 <tr>
	     <td>Sent time</td>   
	     <td>Select **Send by schedule** and specify a reasonable time point down to the second, such as **2020-01-25 00:00:00**. <br>As only a time point within one month can be specified for schedule, please configure the sending task appropriately.</td>   
     </tr> 
	 <tr>
	     <td>Recipient</td>   
	     <td>Click **Download Standard Template**, enter recipient's mobile number and custom SMS content in the form by referring to the <a href="#Table2">sample table</a>, and click **Click here** to upload it. The maximum form size supported is 30 MB.</td>   
     </tr> 
</table>
 Below is a sample table:
 <span id="Table2"></span>
 <table>
     <tr>
         <th width="50%">Recipient's Mobile Number</th>  
         <th>SMS Content Variable 1</th>
		</tr>
	 <tr>      
      <td>Example: 139xxxxxxxx <br>Instructions: please enter the mobile numbers of recipients. All the mobile numbers in one single SMS sending must be registered in Mainland China. The cells need to be in a regular format, i.e., without any specific number formats. </td> 
	     <td>Example: John Smith<br>Instructions: please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>
     </tr> 
</table>
3. Click **OK**.
4. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the status of the task in the Delivery Records list. When the status is **sent**, the task has been completed.

## Step 4. View SMS delivery result
You can view the SMS delivery result in the following ways:
- On the **Chinese Mainland SMS** > **Bulk SMS** page, click **Details & Report Analysis** on the line of the target task to view its detailed record and report analysis.
- Select **Statistics** > **Chinese Mainland SMS** and you can filter and view the statistics and relevant analysis of Chinese Mainland SMS by application, signature, body template, and time.
