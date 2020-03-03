You can grant permissions to each collaborator/sub-account in the console. For the authorization method, please see [CAM](https://intl.cloud.tencent.com/document/product/598/10602).

EMR currently provides three permission roles, which you can search for by the EMR keyword on the policy page in the [CAM Console](https://console.cloud.tencent.com/cam/overview).

| Role | Permissions | 
|---------|---------|
| QcloudEMRObserverAccess (observer access)	| Call the API for getting component configuration information. <br>Call the API for getting monitoring information. <br>Call the API for getting node information. <br>Get the cluster list. |
| QcloudEMROperationAccess (OPS access)	| Inherit the observer access. <br>Modify parameters and distribute configurations. <br>Restart services. <br>Change passwords. |
| QcloudEMRAdministratorAccess (admin access) | Inherit OPS access. <br>Scale out. <br>Scale in. <br>Create clusters. <br>Terminate clusters. <br>Change passwords. |
