
## Verification Mode
### Identity verification overview
Tencent Cloud [identity verification](https://intl.cloud.tencent.com/document/product/378/3629) consists of individual and organization verification. **Different verification modes correspond to different SMS features. We recommend you select an identity verification mode based on your actual account ownership.**

| Type             | Object                           | Account Ownership | Operation Guide                                                     |
| :--------------- | :--------------------------------- | :------- | :----------------------------------------------------------- |
| Individual Verification | Individual                               | Individual      | [Individual Verification Guide](https://intl.cloud.tencent.com/document/product/378/10495) |
| Organization Verification | Enterprises, government, public institutions, schools, and organizations | Organization     | [Organization Verification Guide](https://intl.cloud.tencent.com/document/product/378/10496) |

If you have completed Individual Verification for your account, you can apply for a change to organizational identity. Users who haven't completed identity verification cannot purchase resourcesin the Chinese Mainland.

### Differences in rights

<table>
     <tr>
         <th>Feature</th>  
         <th width="40%">Individual User</th>  
         <th width="40%">Organizational User</th>  
     </tr>
	 <tr>      
         <td>Free package</td>   
	     <td>100 Mainland China SMS messages are gifted free of charge upon activation of the service for the first time</td>   
	     <td>1,000 Mainland China SMS messages are gifted free of charge upon activation of the service for the first time</td>   
     </tr> 
	 <tr>
	     <td>Regular Mainland China SMS</td>   
	     <td>Supported</td>   
	     <td>Supported</td> 
     </tr> 
	 <tr>
	     <td>Marketing Mainland China SMS</td>   
	     <td>Not supported</td>   
	     <td>Supported</td> 
     </tr> 
	 <tr>      
         <td>Global SMS</td>    
	     <td>Supported</td>   
	     <td>Supported</td> 
     </tr>  
	 <tr>      
         <td>Signature type</td>  
	     <td>If the signature is owned by an individual, the following signature types are not supported: <b>company</b>, <b>trademark</b>, and <b>government/public institution/other</b></td>   
	     <td>If the signature is owned by an enterprise or public institution, all signature types are supported</td> 
     </tr> 
	 <tr>      
         <td>Body template</td>
	     <td>A variable can contain up to 12 characters<br>One Chinese character, letter, digit, punctuation mark (in either fullwidth or halfwidth form), or space will be calculated as one character</td>   
	     <td>There is no limit on the number of characters in each variable, but a template cannot contain only variables</td> 
     </tr>     
		      <tr> 
         <td>Custom frequency limit control</td>     
	     <td>Not supported</td>   
	     <td>Supported</td> 
     </tr> 
		      <tr> 
         <td>Signature and body template APIs</td>     
	     <td>Not supported. Signatures and body templates can be managed only in the SMS console</td>   
	     <td>Supported</td> 
     </tr> 		 
</table>


## Review Standards
An SMS message consists of a signature and a body. Before sending an SMS message, you need to create an SMS signature and an SMS body template.

| Component | Description | Review Standard |
|---------|---------|---------|
| Signature | An SMS signature must conform to its owner's attributes. You need to provide the corresponding qualification certificates when creating a signature, which can be used only after it is approved. | [Signature Review Standards](https://intl.cloud.tencent.com/document/product/382/40658) |
| Body content | You must apply for an SMS body template for the SMS content in advance, which can be used only after it is approved. <br>The template allows you to use variables to customize the SMS content, and the message meaning and scenario must be identifiable through the text content (excluding variables). | [Body Template Review Standards](https://intl.cloud.tencent.com/document/product/382/40659) |

## Review Process
### Review duration
Generally, the review result will be returned in about 2 hours after you create an SMS signature or body template (review hours: 9:00–23:00 everyday).
If you urgently need to use the SMS feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will expedite the review.

### Review status description
- Pending review: you have submitted an SMS signature or body template, and it is waiting for review. The review result will be returned in about 2 hours.
- Approved: your SMS signature or body template has been approved. If both of them are approved, you can start sending SMS messages.
 An approved body template does not necessarily mean that messages will be successfully delivered (as ISPs also have sampling-based review mechanisms). If your SMS message fails to be sent, you can consult [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance.
- Rejected: your signature or body template is rejected for some reasons.
  You can log in to the [SMS](https://console.cloud.tencent.com/sms/smsSign/1400054957/0/10) console and click **View Failure Reason and Modify** next to the target signature or template to view the specific reason for rejection. You can also [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Suspension Rules
We will review the SMS signature and body template you create and monitor and check the content of actually sent SMS messages to prevent any violation of applicable national laws and regulations.
If non-compliant SMS content is found, your account will be suspended, and your security deposit will be deducted, or you will be held liable according to the actual situation. After your account is suspended, you cannot continue to use the SMS service and cannot apply for reactivation in the future, and unused SMS service packages in your account cannot be used.
Please strictly comply with the requirements in [SMS Signature Specifications](https://intl.cloud.tencent.com/document/product/382/40658) and [SMS Body Template Specifications](https://intl.cloud.tencent.com/document/product/382/40659), strengthen your business security, and send compliant SMS messages.

