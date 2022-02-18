
## Prerequisites

- The SMS body template has been approved.
- If you want to include a signature in the message, you need to have an approved SMS signature.

## Directions
1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. Select **Global SMS** > **Bulk SMS** on the left sidebar and click **Create Bulk SMS Sending Task**.
4. Configure the following parameters as needed:
 - Template Name: select an approved body template to be used (different templates are distinguished by template name).
 - Signature Name: select an approved SMS signature to be used (different signatures are distinguished by signature name), which is optional.
 - Delivery Time: select **Send Now** or **Send by Schedule**.
 - Recipient: click **Template Download**, enter recipient's mobile number and custom SMS content in the form, and click **Select File** to upload it. The maximum form size supported is 30 MB.
   >Up to 1,000 Global SMS messages can be sent per day under one Tencent Cloud account.
   >
   <table>
     <tr>
         <th width="22.5%">Recipient's Mobile Number</th>  
         <th width="22.5%">SMS Content Variable 1</th>  
         <th width="22.5%">SMS Content Variable 2</th>
				 <th width="10%">……</th>
				 <th>SMS Content Variable N</th>
		</tr>
	 <tr>      
        <td>Example: 139xxxxxxxx <br>Instructions: please enter the mobile numbers of recipients. All the mobile numbers in one single SMS sending must be registered outside Mainland China. The cells need to be in a regular format, i.e., without any specific number formats. </td>   
	     <td>Example: test company A <br>Instructions: please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>   
	     <td>Example: server B <br>Instructions: please enter the second custom variable content according to the body template, i.e., replacing {2} in the template. </td>      
	     <td>……</td>        
	     <td>Example: 100 USD <br>Instructions: please enter the Nth custom variable content according to the body template, i.e., replacing {N} in the template. </td>  
     </tr> 
</table>
 - Application: select the application that needs to send the SMS.
4. Click **OK**.
5. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the status of the task in the Delivery Records list. When the status is **sent**, the task has been completed.

## Subsequent Operations

You can view the SMS delivery result in the following ways:
- On the **Global SMS** > **Bulk SMS** page, click **Details & Report Analysis** on the line of the target task to view its detailed record and report analysis.
- Select **Statistics** > **Global SMS** and you can filter and view the statistics and relevant analysis of Global SMS by application, signature, body template, and time.

## Related Documentation
You can also send SMS via APIs or SDKs. For detailed directions, please see [API documentation](https://intl.cloud.tencent.com/document/product/382/39155) or [SDK documentation](https://intl.cloud.tencent.com/document/product/382/36788).
