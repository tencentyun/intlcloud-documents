## Overview

Filename formatting is a solution that allows users to rename cloud objects that Tencent Cloud Object Storage (COS) provides based on [Serverless Cloud Function (SCF)](https://www.tencentcloud.com/document/product/583). When an object is uploaded to COS, it will be automatically renamed according to your naming convention. You can also replace existing filenames with variable placeholders.

## Notes

- If you have previously added a filename formatting rule to your bucket via the COS console, you can view the filename formatting function you created in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support filename formatting, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, Seoul, Silicon Valley, and more. For more supported regions, see the [SCF documentation](https://www.tencentcloud.com/document/product/583).
- If an error is reported when you rename objects, click **View Log** on the right of the function to quickly redirect to the SCF console to view the error logs.
- Filename formatting is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage class. To rename these objects, you need to restore them first. For detailed directions, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- The filename formatting feature depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF pricing](https://intl.cloud.tencent.com/document/product/583/12281).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **App Integration** > **Extended Features** and find **Filename Formatting**.
3. Click **Configure Formatting Rule** to enter the rule configuration page.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
4. Click **Add Function** and configure the following parameters:

 - **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: COS bucket of the target object.
 - **Event Type**: An operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using PUT method** as the event type, filename formatting will be triggered only for files uploaded via the `PUT Object` API.
 - **Trigger Condition**: The upload path that will trigger SCF. If you select **Specified Range**, SCF will be triggered only when a file is uploaded to a path with the specified prefix or suffix. If you select **The whole bucket**, SCF will be triggered as long as a file is uploaded to any location of the bucket.
 - **SCF Authorization**: For filename formatting, you need to select this option to authorize SCF to read the object from your bucket and change the existing filename.
5. After configuring the information, click **Next** to enter the formatting rule configuration page.

 - **Target Name Format**: Template for the desired name. You can use a default variable in the format of `${variable name}` as the template parameter. The following default variables are supported:
<table>
	<tr><th>Variable Name</th><th>Description</th></tr>
	<tr><td>Bucket</td><td>Name of the associated bucket configured above</td></tr>
	<tr><td>Region</td><td>Region of the associated bucket</td></tr>
	<tr><td>Key</td><td>The `Key` value of the source object in COS, such as `abc/test.jpg`</td></tr>
	<tr><td>InputName</td><td>Filename of the source object (without file extension), such as `test`</td></tr>
	<tr><td>InputNameAndExt</td><td>Filename of the source object (with file extension), such as `test.jpg`</td></tr>
	<tr><td>InputPath</td><td>Directory of the source object, such as `test/`</td></tr>
	<tr><td>Ext</td><td>File extension of the source object, such as `.jpg`</br>Note: This variable contains a `.` by default, so you don't need to add a `.`.</td></tr>
	<tr><td>Year</td><td>Year in the time zone you select</td></tr>
	<tr><td>Month</td><td>Month in the time zone you select</td></tr>
	<tr><td>Day</td><td>Day in the time zone you select</td></tr>
	<tr><td>Hour</td><td>Hour in the time zone you select</td></tr>
	<tr><td>Minute</td><td>Minute in the time zone you select</td></tr>
	<tr><td>Second</td><td>Second in the time zone you select</td></tr>
	<tr><td>CRC64</td><td>CRC64 value of the object</td></tr>
	<tr><td>MD5</td><td>MD5 value of the object</td></tr>
	<tr><td>SHA1</td><td>SHA1 value of the object</td></tr>
	<tr><td>SHA256</td><td>SHA256 value of the object</td></tr>
</table>
 - **Delete Source**: You can select whether to delete the source object after its filename is formatted. This option is set to `No` by default; that is, after the filename is formatted, the object will be saved as a new object and stored in the bucket.
 - **Default Time Zone**: Select your time zone. The default time variable in the name template will be displayed according to the selected time zone; for example, if you select `UTC+08:00`, the default time will be the current month, day, year, hour, minute, and second in the UTC+08:00 time zone.
 - **Callback URL**: You can add a callback address, such as `https://www.callback.com`. After each filename is formatted, the system will send a callback notification to this address.
6. Click **Confirm**.

You can perform the following operations on the created function:
 - Click **Log** to quickly redirect to the SCF console to view the error logs.
 - Click **Details** to view the details of a configured filename formatting function rule.
 - Click **More** > **Edit** to modify a filename formatting rule.
 - Click **More** > **Delete** to delete an unwanted filename formatting function.
