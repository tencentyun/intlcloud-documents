**What is a root account, a sub-user, and a collaborator?**

Generally, a Tencent Cloud account has three identities in CAM:

Root account: a general account identity obtained via direct registration and used for login. This identity exists for all accounts by default.

Sub-user: created by the root account via CAM. It can only be used for login on a specific page. The root account ID, username, and password are required to log in. After login, a sub-user can manage cloud resources under its root account based on its permissions.

Collaborator: an identity for collaborating with a root account. For example, if root account A collaborates with root account B to manage root B’s resources, root account A will be displayed as collaborator after login of root account B.

> On some pages or in some documents, a sub-user or collaborator may be referred as a sub-account.



**What is CAM?**

As a service offered by Tencent Cloud, Cloud Access Management (CAM) helps you manage resources and permissions of your account freely. With CAM, you can create and manage sub-users and collaborators, and use policy management for granular access control of your resources, including resources of DNSPod, Domains, CVM, and other Tencent Cloud services.

[View CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583)



**How to Use CAM?**

Associate a specified user with a preset policy as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) of CAM.

[View CAM directions](https://docs.dnspod.cn/dnspod-cam-manage/)



**No Permission**

![img](https://docs.dnspod.cn/content/images/2021/05/image-5.png)

If "No Permission" is displayed when you operate a feature or a page, it indicates that the current account identity you use is sub-user or collaborator, and the permission to operate this feature is not authorized by the root account.

You are advised to take a screenshot of the pop-up window and send it to the root account admin for authorization.

> You can view the current account identity and the root account on [My Account](https://console.dnspod.cn/account). For more information on how to grant permissions by the root account, see [CAM directions](https://docs.dnspod.cn/dnspod-cam-manage/).



**Sub-User and Collaborator Operations Not Supported**

![img](https://docs.dnspod.cn/content/images/2021/05/image-6.png)

If "Sub-User and Collaborator Operations Not Supported" is displayed when you operate a feature or a page, it means the permission to use this feature cannot be granted in CAM.

In this case, only the root account can operate this feature. Even if a sub-account has been associated with a preset policy, it still cannot operate this feature based on authorization in CAM.

At present, domain parking, domain trading, and D-Monitor cannot be operated by a sub-user or collaborator. They will be gradually supported with the upgrade of the service.

> Note: If a sub-account has been associated with a preset policy, it will have permission to operate these features after they are supported by CAM.

