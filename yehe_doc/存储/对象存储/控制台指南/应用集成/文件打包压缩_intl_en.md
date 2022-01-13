## Overview

COS’s [SCF](https://intl.cloud.tencent.com/document/product/583)-based multi-file zipping feature allows you to add multi-file zipping rules to your bucket. You can specify the URLs of files that need to be zipped, and trigger the cloud function to zip the files and save the generated package to the specified path in the bucket.


## Notes

- The generated package cannot be larger than 50 GB.
- If you have added a multi-file zipping function rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support multi-file zipping, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
- If an error is reported when you perform multi-file zipping, click **View Log** on the right of the function to quickly redirect to the SCF console to view the error logs.
- Multi-file zipping is not supported for files stored in the ARCHIVE or DEEP ARCHIVE storage classes. To zip these files, you need to restore them first. For detailed directions, please see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- Multi-file zipping depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier limit according to [SCF Pricing](https://intl.cloud.tencent.com/document/product/583/12281). Note that the more and larger the files you zip, the more resources will be used; the more often you zip your files, the more calling times will be incurred.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Application Integration** on the left sidebar and then select the **Data Processing** tab.
3. Click **Configure Function** for **Multi-File Zipping** to enter the **Multi-File Zipping** configuration page.
>! If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
4. Click **Add Function** and configure the following parameters:
 - **Function Name**: uniquely identifies a function and cannot be modified after it is created. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Execution Method**: execution method for the function. If you set this field to **Sync**, the execution results will be returned after the zipping task is complete. If you set this field to **Async**, the function will respond directly and execute the zipping task in the background.

 - **Authentication Method**: authentication method for the function
    - If you select **SCF**, you need to trigger the function using a role that has permission to call the function.

    - If you select **No**, you need to select an appropriate API gateway to receive requests. If you don’t have an API gateway in this region, click **Create API Gateway service**, and we will configure an API gateway suitable for this function in this region.

 - **API Gateway Service/API Path/Request Method**: For more information about API gateway configurations, please see [API Gateway Overview](https://intl.cloud.tencent.com/document/product/628/11755).
 - **SCF Authorization**: You need to authorize SCF so that it can read files in your bucket and save the generated package to the specified path.
5. Click **Confirm**.

6. Click **Instructions** to view the field description, where `ClientContext` is in JSON format. For the configuration demo, please see [Using APIs to Zip Files](https://intl.cloud.tencent.com/document/product/436/41619).

7. Click **Next** to go to **Calling Test** page.
8. Click **Start**, and the function will be called as configured. You can view the response of the function in **Response**.

9. You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of multi-file zipping functions. If an error is reported, you can click **View Log** to quickly redirect to the SCF console to view the error log details.
 - Click **Edit** to modify the multi-file zipping rule.
 - Click **Delete** to delete an unwanted multi-file zipping function.
