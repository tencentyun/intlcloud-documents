## Overview

The content moderation feature can automatically block non-compliant files. It only applies to data stored on COS origins rather than data cached on CDN nodes.

This document describes how to promptly block non-compliant data cached in CDN through SCF and API Gateway.

## Directions

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list), select **Functions**, and click **Create** to create a function.
2. Select **Create from scratch** and set the following basic configuration items:

 - Function type: Select **Event-triggered function**.
 - Function name: Enter a custom function name.
 - Region: Select the region of the bucket with the moderation feature enabled.
 - Runtime environment: Select **Python 2.7**.
3. Configure the function code as follows:
 - Submitting method: Select **Local ZIP file** or **Upload a ZIP pack via COS**. You can download the ZIP package [here](https://cos5.cloud.tencent.com/cosbrowser/code/scf/cos_audit_cdn_refresh.zip).
 - Execution: Enter **index.main_handler**.
4. Click **Advanced configuration** to configure **Environment configuration**. You can modify all configuration items except the environment variables as needed.
 - Resource type: CPU
 - MEM: 512 MB
 - Initialization timeout period: 65
 - Execution timeout period: 30
 - Environment variable:
    - CI_AUDITING_CALLBACK: Enter the callback address configured in the callback settings of content moderation here. The callback will be performed only if the callback address is set.
    - CDN_URL: Set the required CDN address to purge the CDN cache.
    - REGION: Set the required region where the bucket resides.
    - BUCKET_ID: Set the required bucket ID (i.e., bucket name), which is used to query the image style. Entering an incorrect value will result in an error during style query.
    - IMAGE_STYLE_SEPARATORS: Set the image style separator if you want to purge image style. You can enter multiple separators consecutively with no need to separate them.
    - CDN_REFRESH_TYPE: Set the image object cache purge method, which is purge by URL by default (that is, only the style will be purged). If you set this variable to **path**, the cache accessed by image processing parameters will be purged. Note that purge by path will remove files with longer filenames containing this filename.
Be sure to configure the above environment variables correctly so that cache purge can work as expected.

5. Select **Execution Role** for **Permission configuration** and click **Create execution role** to enter the **Create custom role** page.
6. Select **Serverless Cloud Function (SCF)** as the role entity and click **Next**.

7. Select the `QcloudCDNFullAccess` and `QcloudCIReadOnlyAccess` role policies and click **Next**.
8. Name the role and click **Complete**.
9. After creating the custom role, go back to the function creation page, refresh the role drop-down list, and select the newly created role.
10. Click **Complete**.
11. Go to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service) to activate the API Gateway service.
12. Create an API gateway as instructed in [Creating APIs Connecting to the SCF Backend](https://intl.cloud.tencent.com/document/product/628/39486).
13. Select **Publish** for **Release Environment** and click **Publish service**.
14. On the content moderation page in the CI console, set callback parameters for image or other target types, and set the address of the API gateway created in the previous step as the callback URL.
15. After the callback is configured, resource cache in CDN will be automatically purged based on the moderation callback result.
