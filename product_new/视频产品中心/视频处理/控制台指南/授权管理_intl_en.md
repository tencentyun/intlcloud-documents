## Operation Scenarios
Because MPS needs to perform read/write operations such as downloading files from, transcoding files in, and uploading files to COS buckets, you need to create service roles and grant MPS permissions to operate on COS resources.

## Directions

1. Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Authorization Management** on the left sidebar to enter the authorization management page. If you have not authorized MPS, click **Go to CAM** to enter the unified permission management page to authorize MPS. After MPS is authorized, the system will create preset service roles and grant MPS relevant permissions.
![](https://main.qcloudimg.com/raw/bafc02e68fdb63bc625d5001cbc2092c.png)
>If you have not completed authorization, you cannot perform further operations in the MPS Console.
2. After authorizing MPS, go back to the authorization management page and you will see that the authorization is completed. If you click **Deauthorize**, you will be directed to the **CAM** page where you can delete [service roles](https://intl.cloud.tencent.com/document/product/598/19388) to revoke MPS' permissions to operate on COS.
![](https://main.qcloudimg.com/raw/631982588decbd10f3ee8753a1193e5e.png)
