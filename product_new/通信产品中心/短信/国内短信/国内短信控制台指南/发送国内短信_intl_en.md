## Prerequisites

- The SMS signature and body template have been approved.
- A sufficient package has been purchased.

## Directions
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Mainland China SMS** > **Bulk SMS** on the left sidebar and click **Create Bulk SMS Task**.
3. Configure the following parameters as needed:
 - Signature Name: Select an approved SMS signature to be used (different signatures are distinguished by signature name).
 - Template Name: Select an approved body template to be used (different templates are distinguished by template name).
 - Delivery Time: Select **Send Now** or **Send by Schedule**.
 - Recipient: Click **Download Template**, enter recipient's mobile number and custom SMS content in the form, and click **Select File** to upload it.
   <table>
     <tr>
         <th width="22.5%">Recipient's Mobile Number</th>  
         <th width="22.5%">SMS Content Variable 1</th>  
         <th width="22.5%">SMS Content Variable 2</th>
				 <th width="10%">……</th>
				 <th>SMS Content Variable N</th>
		</tr>
	 <tr>      
      <td>Example: 9xxxxxxx <br>Instructions: Please enter the mobile numbers of recipients. All the mobile numbers in one single SMS sending must be registered in Mainland China. The cells need to be in a regular format, i.e., without any specific number formats. </td>    
	     <td>Example: Test company A <br>Instructions: Please enter the first custom variable content according to the body template, i.e., replacing {1} in the template. </td>   
	     <td>Example: Server B <br>Instructions: Please enter the second custom variable content according to the body template, i.e., replacing {2} in the template. </td>      
	     <td>……</td>        
	     <td>Example: 100 USD <br>Instructions: Please enter the Nth custom variable content according to the body template, i.e., replacing {N} in the template. </td>  
     </tr> 
</table>
 - Application: Select the application that needs to send the SMS. 
4. Click **Confirm**.
5. Check the number of recipients, indicate your consent to the prompt about fees, and click **Send**.
 You can view the status of the task in the Delivery Records list. When the status is **sent**, the task has been completed.

## Subsequent operations

You can view the SMS delivery result in the following ways:
- On the **Mainland China SMS** > **Bulk SMS** page, click **Details & Report Analysis** on the line of the target task to view its detailed record and report analysis.
- Select **Statistics** > **Mainland China SMS** and you can filter and view the statistics and relevant analysis of Mainland China SMS by application, signature, body template, and time.

## Related documentation
You can also send SMS via APIs or SDKs. For more information, see [API documentation](https://intl.cloud.tencent.com/document/product/382/13297#.E7.9F.AD.E4.BF.A1-api) or [SDK documentation](https://intl.cloud.tencent.com/document/product/382/32991).
