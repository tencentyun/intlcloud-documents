## Overview
COS’s web-based diagnostic tool allows you to troubleshoot error requests. You can enter the error `RequestId` (see [Obtaining RequestId](https://intl.cloud.tencent.com/document/product/436/41230)) on the tool page and click **Diagnose**. The tool will check the request and provide basic information about the request as well as suggestions so that you can quickly troubleshoot COS API errors.

## Tool URL
[Diagnosis Tool](https://console.cloud.tencent.com/cos5/diagnose)

## Directions

1. Click [Diagnosis Tool](https://console.cloud.tencent.com/cos5/diagnose).


2. Enter the `RequestId` and click **Diagnose**.

3. Wait and view the diagnostic result.

The result includes the suggestions and the request information.
 - The suggestions help you quickly locate the COS API errors.
 - The request information is the information about the request corresponding to `RequestId`.

4. Send your feedback on the suggestions.
Click **Helpful** or **Not Helpful** below the suggestions so that we can further improve the tool.


## FAQs

On the diagnostic tool page, you can also find the FAQs. If you have any queries, please [contact us](https://intl.cloud.tencent.com/contact-sales).


## Notes

A COS `RequestId` must:
1. Start with N.
2. Contain at least 30 characters.
3. Comply with the Base64 standard.
