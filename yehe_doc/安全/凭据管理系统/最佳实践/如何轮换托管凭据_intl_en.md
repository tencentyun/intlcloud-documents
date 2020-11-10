To improve system security, the update of a secret needs to be synced across multiple applications and configurations. For a multi-application scenario, if secrets are stored in local files, an application might be missed, running a risk of application interruptions. SSM enables you to apply a secret update to all dependent applications. Also, you can [create multiple versions for a secret](https://intl.cloud.tencent.com/document/product/1078/38603) to implement beta updates and rotation.
![](https://main.qcloudimg.com/raw/4b19949912a67d9984e2c55a18583969.png)
You can rotate secrets in either of the following ways:

  - **Method 1**: Add a secret version. The server can implement beta rotation by updating the secret version. For more information, please see [Managing Multiple Secret Versions](https://intl.cloud.tencent.com/document/product/1078/38603).
![](https://main.qcloudimg.com/raw/6110963be1071da82255ed90d07bde77.png)

- **Method 2**: Update the content of the current secret. When the server calls an API to obtain the secret, the secret content is updated automatically. For more information, please see [Secret API Calling Example](https://intl.cloud.tencent.com/document/product/1078/38616).
