You can grant permissions to each collaborator/sub-account in the console. For the authorization method, see [CAM](https://intl.cloud.tencent.com/document/product/598/10602).

EMR currently provides three permission roles. You can search for the roles by the keyword “EMR” on the policy page in the [CAM Console](https://console.cloud.tencent.com/cam/overview).

| Role | Permissions |
|---------|---------|
| QcloudEMRObserverAccess (observer access)	| API for getting component configuration information. <br>API for getting monitoring information. <br>API for getting node information. <br>Get cluster list. |
| QcloudEMROperationAccess (OPS access)	| Inherit the observer access. <br>Modify parameters and distribute configurations. <br>Restart services. <br>Change passwords. |
| QcloudEMRAdministratorAccess (admin access) | Inherit OPS access. <br>Restart the specified service. <br>Scale out. <br>Scale in. <br>Create a cluster. <br>Terminate the specified cluster. <br>Change passwords for the specified cluster. |
