## Overview

Hash calculation is a solution that allows users to verify the integrity of cloud objects that Tencent Cloud Object Storage (COS) provides based on [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). When an object is uploaded to COS, its hash will be auto-calculated and added to the object's custom header to facilitate integrity verification.

## Notes


- If you have previously added a hash rule to your bucket via the COS console, you can view the hash function you created in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support hash calculation, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
- If an error is reported during hash calculation, click **View Log** on the right of the function to quickly redirect to the SCF console to view the error logs.
- Hash calculation is not supported for files stored in the ARCHIVE or DEEP ARCHIVE storage classes. To calculate the hashes of these files, you need to restore them first. For detailed directions, please see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- The hash calculation feature depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration**. Then, select the **Data Processing** tab and find **Hash Calculation**.
3. Click **Hash Calculation** to go to the rule configuration page.
>! If you haven't activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
4. Click **Configure Hash Rule** and configure the following information in the pop-up window:

 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: identifies the COS bucket where the file whose hash is to be calculated resides.
 - **Event Type**: an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using PUT method** as the event type, hash calculation will be triggered only for files uploaded via the `PUT Object` API.
 - **Trigger Condition**: the upload path that will trigger SCF. If you select **Specified Range**, SCF will be triggered only when a file is uploaded to a path with the specified prefix or suffix. If you choose **The whole bucket**, SCF will be triggered as long as a file is uploaded to any location of the bucket.
 - **SCF Authorization**: to enable hash calculation, you need to select this item to authorize SCF to read the corresponding file from your bucket and add the calculated hash to the custom header of the file.
5. Click **Confirm**.

You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of the hash function. If an error is reported, you can click **View Log** to quickly redirect to the SCF console to view the error log details.
 - Click **Edit** to modify the hash rule.
 - Click **Delete** to delete an unwanted hash function.
