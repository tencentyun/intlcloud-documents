Tencent Container Registry (TCR) is an on-cloud container image hosting service provided by Tencent Cloud. It supports Docker images, Helm chart storage and distribution, and image security scanning and provides fine-grained access permission management and network access control for organizational users. It supports global image sync and triggering, so organizational users can expand their business globally and implement workflow CI/CD with containers. It offers large-scale container clusters with over 1,000 nodes to pull large gigabyte-level images concurrently, ensuring ultra-fast business deployment. With TCR, you can enjoy a secure and efficient image hosting and distribution service in the cloud with no need to build and maintain such service on your own. In addition, TCR can be used together with TKE to deliver a smoother on-cloud container user experience.

TCR operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------|------|------------------------------------|
| Deleting image tags in batches          | tcr  | BatchDeleteImagePersonal           |
| Deleting image repositories in batches          | tcr  | BatchDeleteRepositoryPersonal      |
| Creating Enterprise Edition instance           | tcr  | CreateInstance                     |
| Getting temporary login password          | tcr  | CreateInstanceToken                |
| Creating namespace            | tcr  | CreateNamespacePersonal            |
| Creating image repository for Personal Edition instance     | tcr  | CreateRepositoryPersonal           |
| Creating public network access policy          | tcr  | CreateSecurityPolicy               |
| Deleting the automatic global image tag clearance policy of Personal Edition instance | tcr  | DeleteImageLifecycleGlobalPersonal |
| Deleting image tag            | tcr  | DeleteImagePersonal                |
| Deleting instance              | tcr  | DeleteInstance                     |
| Deleting long-term access credential          | tcr  | DeleteInstanceToken                |
| Deleting namespace            | tcr  | DeleteNamespacePersonal            |
| Deleting image repository            | tcr  | DeleteRepositoryPersonal           |
| Deleting the allowed public network access policy of instance     | tcr  | DeleteSecurityPolicy               |
| Querying long-term access credential information        | tcr  | DescribeInstanceToken              |
| Managing instance public network access          | tcr  | ManageExternalEndpoint             |
| Setting the automatic global image tag clearance policy of Personal Edition instance | tcr  | ManageImageLifecycleGlobalPersonal |
| Managing VPC access over private network for instance       | tcr  | ManageInternalEndpoint             |
| Managing instance sync            | tcr  | ManageReplication                  |
| Updating the long-term access credential of instance        | tcr  | ModifyInstanceToken                |
