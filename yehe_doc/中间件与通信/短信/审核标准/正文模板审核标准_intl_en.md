>!Should you violate the Terms of Service, Tencent Cloud has the right to unilaterally take measures such as restricting, suspending, or terminating the service provided to you or suspending your account (without reactivation) at any time in accordance with the Terms of Service. For subscribed packages, no unsubscription/refund will be allowed, regardless of whether they have been used. Tencent Cloud reserves the right to hold you legally liable for any serious impacts or consequences arising therefrom. Please strictly comply with the Terms of Service, strengthen your business security, and send compliant SMS messages.

Review of an SMS body template generally consists of the following parts:
- [Content review](#content): compliance of the SMS template content is reviewed.
- [Variable review](#variable): compliance of SMS template variables is reviewed.
- [Review based on specific specifications](#special): compliance of different types of SMS messages (notification, verification code, marketing SMS, etc.) with special specifications is reviewed.

## Common Specifications
### Content specifications[](id:content)

| Type | Specification |
|---------|---------|
| Format restrictions | <li>The total length of an SMS message (containing the actual values of the signature and variables) cannot exceed 500 characters. Each Chinese character, letter, digit, punctuation mark (in either fullwidth or halfwidth form), or space will be calculated as one character. </li><li>"[]" is not supported in order to avoid confusion with the signature. </li><li>¥, ★, and special combination symbols entered by keystrokes (such as ^_^&, ☞, &#10003;, and ※) are not supported, as they may cause garbled text in the SMS message.</li> |
| Content specifications | The template must reflect the actual business, and the message meaning and scenario must be identifiable through the text content (excluding variables). <li>Any finance-related content (verification code, notification, and marketing SMS) is prohibited. </li><li>Sending illegal and non-compliant content is prohibited. </li><li>Sending unsolicited invitations, such as invitations for signup or membership, is prohibited. </li><li>For the real estate and education industries, only verification codes can be sent currently. </li><li>Any link in a message must be a URL with an ICP filing in the form of constant (fixed values). </li><li>It is prohibited to send messages related to the following: stock, immigration, job interview, lottery, rebate, lucky draw, loan, debt collection, investment and wealth management, gambling, lottery winning, drugs, politics, legal right protection, crowdfunding, charitable donation, religion, superstition, funeral, click farming, websites for sending empty packages, one-dollar lucky draw, one-dollar flash sales, counterfeit products, healthcare, plastic surgery, beauty, club, bar, foot massage, violence, intimidation, pornography, fur, exam cheating, decoration (including building materials and home furnishings), trademark registration, group joining, friend adding on QQ or WeChat, dating, personal information selling, promotional SMS channel, game promotion, exhibition promotion, website promotion, coupon promotion, card promotion, insurance promotion, credit limit increasing, cashback and rebate, invoice, positive review invitation, alcohol, user acquisition, and user reactivation.</li> |

### Variable specifications[](id:variable)
The SMS body template can contain variables, through which you can enter custom SMS content.

| Type | Specification |
|---------|---------|
| Format | `{Digit}` in the order of `{1}`, `{2}`, and so on. |
| Other specifications | <li>A template cannot contain only variables. </li><li>For body templates created by individual users, the value for each variable can contain up to 12 characters. For those created by organizational users, there is no length limit on the value for each variable. </li><li>A template cannot contain any link variables (including short URLs), such as `www.{1}.com`. </li><li>Variables cannot be used to pass through links (including short URLs), that is, the variable values cannot be set to links (including short URLs). </li> |

## Special Specifications[](id:special)
In addition to the common specifications, there are also special specifications for different types of SMS body templates as detailed below:

<table>
     <tr>
         <th width="20%">SMS Type</th>  
         <th nowrap="nowrap">Content Specification</th>  
     </tr>
	 <tr>      
         <td nowrap="nowrap">Regular SMS (verification code)</td>   
	 <td><li>Chinese Mainland SMS verification code messages must contain the keyword <b>verification code</b>, and Global SMS verification code messages must contain the keyword <b>code</b>. </li><li>The variable in an SMS verification code template can contain only 0–6 digits. </li><li>In addition to the common specifications, it is also prohibited to send marketing and promotional content and links, including internal business promotion information of ISPs.</li></td>   
     </tr> 
	<tr> 
	     <td nowrap="nowrap">Regular SMS (notification)</td>   
	     <td>In addition to the common specifications, it is also prohibited to send marketing and promotional content and links, including internal business promotion information of ISPs.</td>   
     </tr> 
	 <tr>
	     <td>Marketing SMS</td>   
	     <td><li>The body template must have an unsubscription method at the end that supports replying "TD", "T", "N", etc. to unsubscribe. </li><li>In addition to the common specifications, four more types of marketing SMS messages (education, real estate, finance, and loan) are prohibited. </li><li>Marketing SMS messages to non-member users are prohibited in addition to the common specifications. </li><li>Marketing SMS messages should be sent between 8:00 and 22:00 and avoid sending at nighttime as much as possible to reduce user complaints. </li></td>   
     </tr> 
</table>

## Related Information

- [Review process](https://intl.cloud.tencent.com/document/product/382/40653)
- [Suspension rules](https://intl.cloud.tencent.com/document/product/382/40653)
- [Signature review standards](https://intl.cloud.tencent.com/document/product/382/40658)
- [FAQs about body template](https://intl.cloud.tencent.com/document/product/382/13301)

If you have any questions about the body template review standards, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

