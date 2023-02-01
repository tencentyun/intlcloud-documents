When using the EMR service, you need to authorize the default system role `EMR_QCSRole` for the service account. Only after the role is authorized successfully can EMR call relevant services such as CVM and COS to create clusters and store logs.
>!When you activate the EMR service for the first time, you must use the root account to complete role authorization; otherwise, neither sub-accounts nor the root account can use EMR.

## Role authorization process
1. When you create a cluster or a scheduled plan, if the `EMR_QCSRole` role fails to be authorized for the service account and the following prompt is displayed, you need to click **Go to CAM** to complete role authorization.
![](https://main.qcloudimg.com/raw/fec28f413d0423a4e42f57ee838299a2.png)
2. Click **Grant** to authorize the default role `EMR_QCSRole` for the EMR service account.
 ![](https://main.qcloudimg.com/raw/d8ad5786438aba4f5233f6117155e5bc.png)
3. After the authorization, you need to refresh the EMR console or the purchase page. For more information on the policies related to `EMR_QCSRole`, please log in to the [CAM console](https://console.cloud.tencent.com/cam/policy). For more information on the permissions included in `EMR_QCSRole`, please see [Collaborator/Sub-account Permissions](https://intl.cloud.tencent.com/document/product/1026/31100).

## Notes on rule authorization for container-based EMR
1. Before creating a container-based EMR cluster, you need to check whether the `CVM_QCSRole` role exists.
![](https://qcloudimg.tencent-cloud.cn/raw/d85d2817e5aba173cbf28d5a53882eec.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/fa4d943dd9d035c7649fe878516e62b7.jpg)
2. If the `CVM_QCSRole` role does not exist, you need to create it in advance. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role/detail?roleId=4611686018428056826), create a role, and select **Tencent Cloud Product Service**.
![](https://qcloudimg.tencent-cloud.cn/raw/fdb3f045b5bceec298975d4d99c1cfeb.jpg)
3. Select **Cloud Virtual Machine (cvm)** and enter the role name.
![](https://qcloudimg.tencent-cloud.cn/raw/5c092e9bddf48af31c5e2fd6445aa59a.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/a6802504d5cea34f8327d259b3b1e217.jpg)
