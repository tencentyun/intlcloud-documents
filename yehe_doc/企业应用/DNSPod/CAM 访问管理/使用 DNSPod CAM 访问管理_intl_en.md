The DNSPod console has fully integrated Tencent Cloud CAM. You can use a CAM policy to authorize a sub-user or collaborator to access (read-only or full) a specified domain.

**About CAM**

As a service offered by Tencent Cloud, Cloud Access Management (CAM) helps you manage resources and permissions of your account freely. With CAM, you can create and manage sub-user and collaborator accounts, and use policy management for granular access control of your resources, including resources of DNSPod, Domains, CVM, and other Tencent Cloud services.

[View CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583)

**How to Use CAM**

Associate a specified user with a preset policy as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) of CAM.

Read-only access to DNSPod resources: QcloudDNSPodReadOnlyAccess

Full read-write access to DNSPod resources: QcloudDNSPodFullAccess

> Note: The above two preset policies cover all DNSPod resources under the account, such as DNS and paid plans.

> Read-only access to DNSPod resources means that a user is authorized to view but not edit or modify resources. For example, the user can view the DNS records of a domain, but not modify them.

> Full read-write access to DNSPod resources means that a user is authorized to view, modify, and manage resources. For example, the user can modify DNS records, delete domains, and perform other operations, but not set accounts or perform operations in the Billing Center.