When using the EMR service, you need to authorize the default system role `EMR_QCSRole` for the service account. Only after the role is authorized successfully can EMR call relevant services such as CVM and COS to create clusters and store logs.
>When you activate the EMR service for the first time, you must use the root account to complete role authorization; otherwise, neither sub-accounts nor the root account can use EMR.

## Role Authorization Process
1. When you create a cluster or a scheduled plan, if the `EMR_QCSRole` role fails to be authorized for the service account and the following prompt is displayed, you need to click **Go to CAM** to complete role authorization.

2. Click **Authorize** to authorize the default role `EMR_QCSRole` for the EMR service account.
 
3. After the authorization, you need to refresh the EMR Console or the purchase page. For more information on the policies related to `EMR_QCSRole`, please log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy). For more information on the permissions included in `EMR_QCSRole`, please see [Collaborator/Sub-account Permissions](https://intl.cloud.tencent.com/document/product/1026/31100).
