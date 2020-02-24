## Introduction
MPS needs to perform read/write operations, including downloading, transcoding and uploading for files in COS buckets. Therefore, you need to create service roles and grant MPS permissions to operate on COS resources.

## Directions

1. Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Authorization Management** on the left sidebar. If you have not authorized MPS, click **Go to CAM** to enter the permission management page to authorize MPS. After MPS is authorized, the system will create preset service roles and grant MPS relevant permissions.
![](https://main.qcloudimg.com/raw/4e037db82d7e9849fbba3af4ab32ccc5.png)
>If you have not completed authorization, you cannot perform further operations in the MPS Console.
2. After authorizing MPS, go back to the authorization management page and you will see that the authorization is completed. If you click **Cancel Authorization**, you will be directed to the **CAM** management page where you can delete the [service roles](https://intl.cloud.tencent.com/document/product/598/19388) to revoke MPS' permissions to operate on COS.
![](https://main.qcloudimg.com/raw/d1457827ae9b3416cffc03f76d0fe99f.png)
