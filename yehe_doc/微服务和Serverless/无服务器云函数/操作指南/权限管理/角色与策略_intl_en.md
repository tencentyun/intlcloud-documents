
## Concepts
#### Roles
A [role](https://intl.cloud.tencent.com/document/product/598/19420) is a virtual identity with a set of permissions provided by Tencent [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583), which can be associated with policies to grant access permissions of services, actions (operations), and resources in Tencent Cloud to [role entities](https://intl.cloud.tencent.com/document/product/598/19421). After these permissions are added to a role, the role can be configured to Tencent Cloud services, allowing the services to perform operations on authorized resources on your behalf. SCF offers **configuration roles** and **execution roles**. You can use the configuration role to enable SCF to access user resources in the configuration process. You can also use the execution role to enable SCF to apply for the temporary authorization for executing the code, so that the code can implement permission and resource access through the role authorization mechanism.

#### Policies
A [policy](https://intl.cloud.tencent.com/document/product/598/10600) is a syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policies and custom policies. The former is some common permission sets created and managed by Tencent Cloud, such as super admin and cloud resource admin, which are read-only and cannot be written. The latter is user-defined permission sets that describe resource management in a more refined way. The former cannot specifically describe individual resources and has a coarse granularity, while the latter can flexibly meet differentiated permission management needs.

#### Permissions
A [permission](https://intl.cloud.tencent.com/document/product/598/10600) describes whether to allow or refuse the execution of certain operations to access certain resources under certain conditions. By default, a root account is the resource owner and has full access to all resources under it, while a sub-account does not have access to any resources. A resource creator does not automatically possess the access to the created resource and should be authorized by the resource owner instead.

## Overview
When creating an SCF function, you may manipulate certain Tencent Cloud services other than SCF. Different operations may require different permissions, such as COS permissions to create and delete COS triggers, API Gateway permissions to create and delete API Gateway triggers, and COS permissions to read zipped code packages, which can be granted by configuring and selecting roles.

## Configuration Roles
A configuration role is used to grant the SCF configuration the permissions to connect with other Tencent Cloud resources to access such resources within the scope of the permissions in the associated policies, including but not limited to code file access and trigger configuration. The preset policy of the configuration role supports the basic operations of function execution and covers the basic permissions required in common SCF scenarios.

### Role details
The default configuration role of SCF is `SCF_QcsRole`, as detailed below:
- Role name: `SCF_QcsRole` 
- Role entity: `service-scf.qcloud.com`
- Role description: SCF default configuration role. This service role is used to grant the SCF configuration the permissions to connect with other resources in the cloud, including but not limited to code file access and trigger configuration. The preset policy of the configuration role can support the basic operations of function execution.
- Associated policies: This role is associated with the `QcloudAccessForScfRole` policy, which can:
 - Write trigger configuration information to the bucket configuration when a COS trigger is configured.   
 - Read the trigger configuration information from the COS bucket.   
 - Read the code zip package from the bucket when the code is updated through COS.   
 - Create API Gateway services and APIs and publish services when an API Gateway trigger is configured.   
 - Perform operations such as configuring and using CLS read/write access.
 - Perform operations such as configuring and using CMQ read/write access.
 - Perform operations such as configuring and using CKafka read/write access.

>!You can log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) to view and modify the policies associated with the current configuration role `SCF_QcsRole`. However, modifying the associated policies may cause SCF to fail. Therefore, we do not recommend modifying the associated policies.
>

### Service authorization
1. If you are using SCF for the first time, you will be prompted for service authorization when you open the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1), as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4ak3401_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219152932.png)

2. Select **Go to CAM** to enter the **Role Management** page and click **Grant** to confirm the authorization as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/uHMx304_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219152948.png)

3. After the authorization is confirmed, the role `SCF_QcsRole` will be automatically created for you as shown below, which can be viewed in [Roles](https://console.cloud.tencent.com/cam/role): 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3mNf507_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219153048.png)

## Execution Roles
An execution role is used for user code, and the role entity is `service-scf.qcloud.com`. After you add the corresponding execution role to the function, SCF will apply for the temporary authorization for your code to run within the scope of the permissions in the policies associated with the execution role, so that the code can get the required permissions and access other Tencent Cloud resources through the role authorization mechanism.
Take `SCF_QcsRole` as an example. You can also select `SCF_QcsRole` as the function execution role to grant the corresponding permissions of the policies associated with the `SCF_QcsRole` to SCF, so that SCF can get the permission to apply for access to other Tencent Cloud resources for your code.

### Creating execution roles
1. Log in to the SCF console and select **[Functions](https://console.cloud.tencent.com/scf)** on the left sidebar.
2. On the "Functions" list page, click the name of the target function to access the function configuration page.
3. Select **Edit** in the top-right corner of the **Function configuration** page.
4. Select **Enable** in **Execution Role** and click **Create execution role** as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/YJ4T410_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219153445.png)
5. In the **Enter Role Entity Info** step, select **Serverless Cloud Function (scf)** and click **Next**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/y4SZ614_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219153607.png)
6. In the **Configure Role Policy** step, select all the policies required by the function and click **Next** as shown below: 
>? This document uses the selection of `QcloudCOSFullAccess` (full access permissions of COS) as an example. Select the policies as needed.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/x6aa519_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219153740.png)

7. Enter a role name in the **Review** step and click **Complete**. This document uses the role name `scf_cos_full_access` as an example.   
8. Return to the function configuration page and click <img src="https://main.qcloudimg.com/raw/b32932fe6f9afabb88280c38bb287887.png" style="margin:-3px 0px"> on the right of "Execution Role" to select the execution role created just now in the drop-down list, as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9d9R722_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219154143.png)
>! When adding policies to an execution role, in addition to preset policies, you can also select custom policies to configure permissions in a more refined manner. SCF's policy syntax follows CAM's [syntax structure](https://intl.cloud.tencent.com/document/product/598/10604) and [resource description method](https://intl.cloud.tencent.com/document/product/598/10606), which is based on the JSON format. For more information, see [SCF Policy Syntax](https://intl.cloud.tencent.com/document/product/583/38177).
>

### Getting the temporary key information of an execution role
When a function is running, the SCF service will use the selected execution role to apply for the temporary `SecretId`, `SecretKey`, and `SesstionToken`.

- For **functions not created based on image**:
They are passed in to the runtime environment in the form of environment variable as shown below: 
![](https://main.qcloudimg.com/raw/04d1d326e4a383d44c4d019a2207ba6e.png)
Take Python as an example. You can run the following code to pass in the above information to the function runtime environment and get it in the form of environment variables:
```python
secret_id = os.environ.get('TENCENTCLOUD_SECRETID')
secret_key = os.environ.get('TENCENTCLOUD_SECRETKEY')
token= os.environ.get('TENCENTCLOUD_SESSIONTOKEN')
```

- For **functions created based on image**:
They are passed in to the input parameter `context` in the form of HTTP header. For more information, see [Feature Description](https://intl.cloud.tencent.com/document/product/583/41076).
