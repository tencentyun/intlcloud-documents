## Overview

COS launched the object concatenation feature based on [Serverless Cloud Function (SCF)](https://www.tencentcloud.com/document/product/583) to allow users to concatenate the binary of multiple objects in a specific order to get a new object.

You need to add an object concatenation rule to a bucket, specify the URLs of objects to concatenate, trigger SCF to perform the concatenation, and store the concatenated object to a specified path in the bucket.


## Notes

- The concatenated object cannot be larger than 50 TB.
- This feature can concatenate only binary of objects and cannot be used to splice audio, videos, or images.
- If you have added an object concatenation rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Object concatenation is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF documentation](https://www.tencentcloud.com/document/product/583).
- If an error is reported when you concatenate objects, click **View Log** on the right of the function to quickly redirect to the SCF console to view the error logs.
- Object concatenation is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To concatenate these objects, you need to restore them first. For detailed directions, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- Object concatenation depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier limit according to [SCF pricing](https://intl.cloud.tencent.com/document/product/583/12281). Note that the more objects you concatenate, the more resources will be used; the more often you concatenate objects, the more calling times will be incurred.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **App Integration** > **Extended Features** and find **Object Concatenation**.
3. Click **Configure API Access** to enter the **Object Concatenation** configuration page.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
4. Click **Add Function** and configure the following parameters:
 - **Function Name**: Uniquely identifies a function and cannot be modified after it is created. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Execution Method**: Execution method for the function. If you set this field to **Sync**, the execution results will be returned after the concatenation task is complete. If you set this field to **Async**, the function will respond directly and execute the concatenation task in the background.
 ![img](https://qcloudimg.tencent-cloud.cn/raw/bebd7661688228c917c8e33e2eee2021.png)
 - **Authentication Method**: Authentication method for the function
    - If you select **SCF**, you need to trigger the function using a role that has permission to call the function.
    - If you select **No**, you need to select an appropriate API gateway to receive requests. If you don't have an API gateway in this region, click **Create API Gateway service**, and we will configure an API gateway suitable for this function in this region.
 - **API Gateway Service/API Path/Request Method**: For more information on API gateway configurations, see [Overview](https://intl.cloud.tencent.com/document/product/628/11755).
 - **SCF Authorization**: You need to authorize SCF so that it can read objects in your bucket and save the concatenated object to the specified path.
5. Click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/7da27a3179c3b061e9063eaa8265d0d6.png)
6. Click **Instructions** to view the field description, where **Request Body** is in JSON format. For the configuration demo, see [Using APIs to Merge Files](https://intl.cloud.tencent.com/document/product/436/42533).
![](https://qcloudimg.tencent-cloud.cn/raw/ce8b8c37806c09fff61a9d39f587e5fa.png)
7. Click **Next** to go to **Calling Test** page.
8. Click **Start**, and the function will be called as configured. You can view the response of the function in **Response**.
![](https://qcloudimg.tencent-cloud.cn/raw/f0b9865f0fc56f17dcb6926d12fffd3a.png)
9. You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of the object concatenation function. If an error is reported, you can click **Log** to quickly redirect to the SCF console to view the error log details.
 - Click **More** > **Edit** to modify an object concatenation function.
 - Click **More** > **Delete** to delete an unwanted object concatenation function.


