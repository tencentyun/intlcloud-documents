## Concepts
Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage the access permissions of resources under your Tencent Cloud account. With CAM, you can create, manage, and terminate users (groups) and use identity and policy management to control user access to Tencent Cloud resources.

## Granting Access
You can grant access permissions by specifying a user to perform a specified action on specified resources under a specified condition. Generally, the following four elements are used to describe an access policy: **principal, resource, action, and condition (optional)**.

## Access Authorization Elements
### Tencent Cloud identity
When you sign up for a Tencent Cloud account, the system creates a root account identity for you to log in to the Tencent Cloud services. With the root account, you can use the user management feature to manage different user types, such as **collaborator, message recipient, sub-user, and role**. For specific definitions, see [Glossary](https://intl.cloud.tencent.com/document/product/598/18564).

### CDWPG cluster resource
CDWPG resources refer to the clusters of Cloud Data Warehouse for PostgreSQL (CDWPG), which are also the objects of access control. Usually, you can see the CDWPG identifier in the console as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6a6042bc2ea6d839b5e160a9cbbc7cab.png)
Here, `snova-28fg7yl3` is the unique cluster identifier, which can also be seen as the identifier of the CDWPG resource.


### CDWPG cluster action
Cluster actions are performed by users in the CDWPG console. Basically, each action can be mapped to a TencentCloud API, such as deleting a cluster and viewing cluster details. Each action has an `action` identifier that can be used for its access control (read and write).

### Principle of least privilege
You must specify the scope of the permission granted to the **specified user** for performing **what actions** and access **what resources** under **what conditions**.


