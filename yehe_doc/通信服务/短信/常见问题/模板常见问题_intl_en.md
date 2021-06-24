### What should I do if an SMS message is rejected with the error "Currently, messages in XX type cannot be send"?
Please check whether the template contains non-compliant content. For more information on the banned industries and content, please see [Body Template Review Standards](https://intl.cloud.tencent.com/document/product/382/40659).

### How do I know what types of SMS messages can be sent and what cannot?

Please apply for signatures and templates in compliance with the [signature](https://intl.cloud.tencent.com/document/product/382/40658) and [body template](https://intl.cloud.tencent.com/document/product/382/40659) review standards.

### How do I enter the template name?
You can enter a template name as needed, and there are no special requirements.

### What should I enter as the template remarks?
If the template content is short, has unclear definition, or has too many variables, you need to add remarks for the use case; otherwise, the review personnel may not be able to confirm the SMS content and use case.
For example, if the template content is `Your verification code is {1}. Please enter it in {2} minutes. If you did not make this request, please contact the customer service at {3}.`, you can enter "Your verification code is 123456. Please enter it 5 minutes. If you did not make this request, please contact the customer service at XXXX." as the template remarks.

### Can I directly enter a link as a template parameter?
You cannot enter links (including short URLs) as a template variable parameter. If required, we recommend you directly use a URL with ICP filing as a constant in the SMS template and use it after the template is approved.

### Is there a limit on the number of SMS templates?[](id:Q6)
You can have up to 200 SMS templates. You can select different templates to send SMS messages as needed.

### Is there a limit on the number of characters in each variable in an SMS body template?
- In an SMS body template created by an individual user, each variable can contain up to 12 characters, and a template cannot contain only variables.
- For organizational users, there is no limit on the number of characters in each variable, but a template cannot contain only variables.

For more information, please see [Variable Specifications](https://intl.cloud.tencent.com/document/product/382/40659#variable).

### Can I add hyperlinks in SMS content?
Yes. Hyperlinks can be added to both general and marketing SMS messages. The link address can be a constant only (fixed), and the SMS content needs to be submitted for review and can be sent only after approval. If the SMS content is found violating the Tencent Cloud SMS Service Agreement, your account will be banned.


### How long does it take to review an SMS message application?
Generally, the review result will be returned in about 2 hours after you apply for an SMS signature or body template (review hours: 9:00–23:00 everyday).
If you urgently need to use the SMS feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will expedite the review.
An approved body template does not necessarily mean that messages will be successfully delivered (as ISPs also have sampling-based review mechanisms). If your SMS message fails to be sent, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### What should I do if the number of characters in an SMS template variable exceeds the limit?
For individual users, a template variable currently can contain up to 12 characters. If the limit is exceeded, we recommend you upgrade to organizational user.

### What is the format of the curly brackets in template variables? How do I enter variables?
Please use `{digit}` as variables in the order of `{1}`, `{2}`, and so on.
For example, `Your verification code is {1}, which is valid for {2} minutes and should not be disclosed to others. If you did not make this request, please ignore this message.`

### Can I modify an SMS template?
Approved templates cannot be modified. If needed, you can submit a new one for review. Templates that are being reviewed or have been rejected can be modified.


### Can I use variables in an SMS body template?
Variable content (such as name, date, and verification code) in an SMS template can be replaced with a variable parameter `{1}`. If there are multiple variables, you need to enter them starting from 1; however, a template cannot contain only variables.

### My SMS body template did not pass the review, and I was prompted to add "Reply "TD" to unsubscribe". Why did this happen?
A body template for marketing SMS messages must contain the unsubscription method so as to allow recipients to reply "TD", "T", or "N" to unsubscribe; otherwise, the messages may be blocked by ISPs.


