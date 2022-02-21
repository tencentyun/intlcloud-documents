### What should I do if my signature application is rejected?

You need to provide corresponding qualification certificates to apply for an SMS signature. Please enter the signature content again and upload correct and authentic certificates according to the [Signature Review Standards](https://intl.cloud.tencent.com/document/product/382/40658).

### Why is the rejection reason " non-identifiable signatures"?

A non-identifiable signature is a signature in which the relevant organizational or individual identity cannot be identified. For example, you cannot use `test`, `aabb`, `verification code`, or `notification` as a signature. We recommend you use the name of your organization or application as the signature. For more information, please see [Signature Review Standards](https://intl.cloud.tencent.com/document/product/382/40658).

### Is there a limit on the number of SMS signatures?
You can apply for up to 50 SMS signatures. To apply for multiple signatures, you need to provide corresponding qualification certificates for each signature.

### Can I modify an SMS signature?
Approved signatures cannot be modified. You can create multiple signatures and select an appropriate one when sending messages.

### How do I apply for a signature when my product is in beta test and cannot be released?
If your product has not been released, please use your organization name to apply for a signature for product testing. After it is released, you can apply for a signature containing your product name.

### Why can't my SMS signature application pass the review?

There are many possible reasons; for example, the signature does not meet the submitted certificates or relevant certificates have not been uploaded. Please apply for an appropriate signature as instructed on the signature application page according to the [signature review standards](https://intl.cloud.tencent.com/document/product/382/40658).

### What should I enter as signature remarks?
You need to enter **application description** only when the signature type is one of the following:
- Application: enter a link to the display page of the application on any application store/market.
- Website: enter the website domain name that has an ICP filing.
- WeChat Official Account (or WeChat Mini Program): enter the full name of the WeChat Official Account (or WeChat Mini Program).

### How do I specify a signature when calling an API to send a message if I have multiple signatures?[](id:Q8)
When calling the [SendSms](https://intl.cloud.tencent.com/document/product/382/34859) API, you can set the `sign` field to select the needed SMS signature.
 For example, if you have two signatures `Tencent Technology` and `Tencent Cloud` and need to send SMS messages with the latter, you only need to set the `sign` field to `Tencent Cloud` and call the corresponding API to send messages.

### What documents should I prepare when applying for an SMS signature?[](id:Q9)
You should prepare different documents according to your SMS signature purpose and account type. For more information, please see [Certificate File List](https://intl.cloud.tencent.com/document/product/382/40658#.E8.AF.81.E6.98.8E.E6.96.87.E4.BB.B6.E8.A7.84.E8.8C.83).

### Can individual users apply for SMS signatures?[](id:Q10)
Individual users can click **[Create Signature](https://console.cloud.tencent.com/smsv2/csms-sign)** in **Chinese Mainland SMS** > **Signatures** in the **console**. However, they also need to submit corresponding certificates. For more information, please see [Certificate File List](https://intl.cloud.tencent.com/document/product/382/40658#.E4.B8.AA.E4.BA.BA.E8.AE.A4.E8.AF.81.E7.94.A8.E6.88.B7).



[](id:Q11)
### How do individual users apply for SMS signatures?
When you apply for an SMS signature as an individual user, we recommend you use the name of your launched application, WeChat Official Account, WeChat Mini Program, or website filed with the MIIT as the signature and provide corresponding certificates.
When creating a signature for self-use, you need to upload the following certificate materials:
 <table>
<tr>
<th>Signature Type</th>
<th>Certificate File</th>
</tr>
<tr>
<td>App</td>
<td>You need to upload a <b>screenshot of the application store/market backend</b></td>
</tr>
<tr>
<td>Website</td>
<td>You need to upload a <b>screenshot of the website ICP filing backend</b></td>
</tr>
<tr>
<td>WeChat Official Account or WeChat Mini Program</td>
<td>You need to upload a <b>screenshot of the ownership of the WeChat Official Account or WeChat Mini Program</b>: <ul><li>WeChat Official Account: screenshot of the **Account Information** > **Account Details** page</li><li>WeChat Mini Program: screenshot of the **Settings** > **Basic Settings** page</li></ul></td>
</tr>
</table>

[](id:Q12)
### How do I apply for an SMS signature if I need to help an enterprise or public institution send SMS messages?
Currently, only enterprises and public institutions are allowed to authorize others to apply for a signature for them. The signature type should be selected as **For unverified entities**, and the following [certificates](https://intl.cloud.tencent.com/document/product/382/40658#.E8.AF.81.E6.98.8E.E6.96.87.E4.BB.B6.E6.B8.85.E5.8D.95.EF.BC.88.E4.BB.96.E7.94.A8.E7.AD.BE.E5.90.8D.EF.BC.89) should be uploaded:
>?Currently, only enterprises and public institutions are allowed to authorize others to apply for a signature for them.

 <table>
<tr>
<th>Signature Type</th>
<th>Certificate File</th>
</tr>
<tr>
<td>Company</td>
<td rowspan="4">You need to upload the <b><a href="https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx">authorization letter</a> </b>and one of the following enterprise and public institution certificates<b> of the entity that owns the signature: </b><ul><li>Three-in-One</li><li>Business license</li><li>Organization code certificate</li><li>Social credit code certificate</li></ul></td>
</tr>
<tr>
<td>App</td>
</tr>
<tr>
<td>Website</td>
</tr>
<tr>
<td>WeChat Official Account or WeChat Mini Program</td>
</tr>
<tr>
<td>Trademark</td>
<td>You need to upload the <b><a href="https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx">authorization letter</a></b> and <b>trademark registration certificate</b></td>
</tr>
<tr>
<td nowrap="nowrap">Government/public institution/other</td>
<td>You need to upload the <b><a href="https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx">authorization letter</a> </b>and one of the following <b>enterprise and public institution certificates</b> of the entity that owns the signature: <ul><li>Organization code certificate</li><li>Social credit code certificate</li><li>Legal person certificate of public institution</li></ul></td>
</tr>
</table>
