<table>
   <tr>
      <th width="0px" style="text-align:center">Error Category</td>
      <th width="0px" style="text-align:center">Error Subcategory</td>
      <th width="0px"  style="text-align:center">Description</td>
      <th width="0px"  style="text-align:center">Solution</td>
   </tr>
   <tr>
      <td style="text-align:center">SMS Type Error</td>
      <td>Incorrect SMS type</td>
      <td>Specify the SMS type as notification for a marketing message.</td>
      <td>Select a correct SMS type according to message content.</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='9'>SMS Content Error</td>
      <td rowspan='2'>Incorrect variable format</td>
      <td rowspan='2'>Incorrect variable format</td>
      <td>Use “{digit}” (in halfwidth form) as variables in the order of “{1}”, “{2}”, and so on.</td>
   </tr>
	    <tr>
      <td>Do not set local variables such as “www.${1}.cn” and “186${2}1234”.</td>
   </tr>
   <tr>
      <td style="text-align:center">Containing unsupported symbols.</td>
      <td>Unsupported symbols (such as ￥, ★, ^_^, &, √, and ※) may result in garbled message content.</td>
      <td><li>Delete unsupported symbols in a template.</li><br><li>Delete the “【】” symbol in the template. Otherwise, the message may not be successfully delivered.</li><br></td>
   </tr>
   <tr>
      <td style="text-align:center">Unclear content.</td>
      <td>A variable-only template, or a template that contains few fixed texts and too many variables. The values of variables are too large, making it hard to identify the business scenario.</td>
      <td>A variable-only template is not supported. Please set variables based on your actual needs and use as many fixed texts as possible to make the message content and the business scenario more identifiable.</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Lacking required keywords.
</td>
      <td >No unsubscription keyword (TD, T, or N) is contained in a marketing message.</td>
      <td>A marketing message must contain a keyword (TD, T, or N) so that recipients can reply to the message with the keyword to unsubscribe.</td>
   </tr>
   <tr>
      <td>The keyword “验证码” is not contained in Chinese mainland verification code messages, or the keyword “code” is not contained in global verification code messages.</td>
      <td>Please add the keyword “验证码” to Chinese mainland verification code messages and the keyword “code” to global verification code messages.</td>
   </tr>
   <tr>
      <td style="text-align:center">Containing forbidden content.</td>
      <td>In addition to notification content, a notification message also contains marketing content.</td>
      <td>Please delete the marketing content.</td>
   </tr>
   <tr>
      <td style="text-align:center">Containing other variables.</td>
      <td>In addition to the verification code, a verification code message also contains other long variables.</td>
      <td>Please do not set other content as variables. Apply for the verification code message templates for registration and password modification separately.</td>
   </tr>
   <tr>
      <td style="text-align:center">The link in a message is invalid or non-compliant.</td>
      <td>The link is irrelevant to the message content, or the link is invalid./td>
      <td><li>Only fixed-text links are supported so that we can review the link content.</li><br><li>If the link is invalid or cannot be opened, please check whether it is correct first.</li><br><li>If the link content is inconsistent with the template content, the message cannot be sent.</li></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='10'>Unsupported or Non-compliant SMS Content</td>
      <td>Content related to recruitment interview is not supported</td>
      <td>-</td>
      <td>Currently, recruitment or interview notification messages cannot be sent.</td>
   </tr>
   <tr>
      <td style="text-align:center">Content related to games, finance, insurance, etc, is not supported.</td>
      <td>-</td>
      <td>Currently, messages related to games, finance, and insurance, cannot be sent.</td>
   </tr>
   <tr>
      <td style="text-align:center">Dating content is not supported.</td>
      <td>-</td>
      <td>Currently, dating messages cannot be sent.</td>
   </tr>
   <tr>
      <td style="text-align:center">Payment reminder messages cannot be sent.</td>
      <td>-</td>
      <td>Payment reminder messages cannot be sent.</td>
   </tr>
   <tr>
      <td style="text-align:center">For the real estate or education industry, only verification code messages can be sent.</td>
      <td>-</td>
      <td>For the real estate or education industry, only verification code messages can be sent, while notification or marketing messages cannot.</td>
   </tr>
   <tr>
      <td style="text-align:center">The template involves content types that are forbidden in Body Template Review Standards.</td>
      <td>-</td>
      <td>It is prohibited to send messages related to the following contents: stock, migration, recruitment interview, lottery, rebate, lucky draw, loan, dunning, credit investigation, investment and wealth management, gambling, lottery winning, drugs, politics, legal right protection, crowdfunding, charitable donation, religion, superstition, funeral, click farming, websites for sending empty packages, one-dollar lucky draw, one-dollar flash sales, counterfeit products, healthcare, plastic surgery, beauty, club, bar, foot massage, violence, intimidation, pornography, fur, exam cheating, decoration (including building materials and home furnishings), trademark registration, group joining, friend adding on QQ or WeChat, dating, personal information selling, promotional SMS channel, game promotion, exhibition promotion, website promotion, coupon promotion, card promotion, insurance promotion, credit limit increasing, cashback and rebate, invoice issuance, positive review invitation, alcohol, user acquisition, and user reactivation. An SMS template containing any of the above content will be rejected.</td>
   </tr>
   <tr>
      <td style="text-align:center">A link is used as a variable.</td>
      <td>-</td>
      <td>A link cannot be used as a variable. Please use it as fixed text.</td>
   </tr>
   <tr>
      <td style="text-align:center">SMS bombing.</td>
      <td>The template contains promotional and user acquisition content without member description.</td>
      <td><li>Add the member name to the template to confirm membership.</li><br><li>It is not allowed to send an SMS message with content such as opening promotion, business introduction, or company promotion. Such message will be regarded as a bombing because its recipient’s membership cannot be verified.</li><br></td>
   </tr>
   <tr>
      <td style="text-align:center">Out-of-date content.</td>
      <td>For example, a promotional template designed for an important festival is submitted after the festival has passed.</td>
      <td>Any festival advertising template (such as May Day or China's National Day) must be submitted for approval ahead of time. Otherwise, the message may not be delivered timely.</td>
   </tr>
</table>
