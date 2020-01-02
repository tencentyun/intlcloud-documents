## Overview of the TKE Image Service Permissions

The address format for TKE image is as follows: `ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}`.
The following fields are required for configuring the permissions of an image repository:

- `${namespace}`: The namespace to which the image repository belongs.
- `${name}`: The name of the image repository.

> Note: 
> Do not include slashes (/) in the namespace `${namespace}` and the image name `${name}`.
> The `${tag}` field currently is only for authenticating the permissions for deleting. For more information, see [Image Tag Permissions](#Tag).
>
> `${namespace}` and `${name}` fields allow you to develop detailed permission schemes for managers to flexibly manage access permissions.  
> For example:

- Permit collaborator A to pull images
- Forbid collaborator A from deleting images
- Forbid collaborator B from pulling images in namespace ns1

If you do not need to manage image repository permissions in detail, you can use [Presetting Policy Authorization](#PresetPolicyAuthorization).
If you need to manage image repository permissions in detail, use [Customizing Policy Authorization](#CustomPolicyAuthorization).
The TKE image service utilizes Cloud Access Management (CAM) to manage access permissions. You can learn more about how to use CAM here:

- [User management](https://intl.cloud.tencent.com/document/product/598/10599)
- [Policy management](https://intl.cloud.tencent.com/document/product/598/10601)
- [Authorization management](https://intl.cloud.tencent.com/document/product/598/10602)

<span id="PresetPpolicyAuthorization"></span>

## Preset Policy Authorization

To simplify TKE image service permission management, the TKE image service has two preset policies:

- [Image repository (CCR) full read/write permission](https://console.cloud.tencent.com/cam/policy/detail/419082&QcloudCCRFullAccess&2)
  The preset policy configures all the permissions of the TKE image service. If the collaborator is associated with the preset policy, they will have the same image repository permissions as the administrator. For more information, see [Permissions List](https://intl.cloud.tencent.com/document/product/457/11528).
- [Image repository read-only permission](https://console.cloud.tencent.com/cam/policy/detail/419084&QcloudCCRReadOnlyAccess&2)
  This preset policy includes only the read-only permission for the TKE image service. If a collaborator is **only** associated with this policy in the TKE image service, the following operations will be prohibited:
- Pushing an image using `docker push`
- Creating an image repository namespace
- Deleting an image repository namespace
- Creating an image repository
- Deleting an image repository
- Deleting an image tag

For information about how to associate a preset policy with a collaborator, see the following CAM documents: [Preset Policy Overview](https://intl.cloud.tencent.com/document/product/598/10601#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5) and [Associating a User with a Preset Policy](https://intl.cloud.tencent.com/document/product/598/10602#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5.E5.85.B3.E8.81.94.E7.94.A8.E6.88.B7).

<span id="CustomPolicyAuthorization"></span>

## Custom Policy Authorization

With a custom policy, the manager can associate different permissions with different collaborators.
Take the following factors into account when assigning permissions:

- **resource**: Which Image Registries are associated with this permission policy. For example, all Image Registries are described as `qcs::ccr:::repo/*`. For more information, see [CAM Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).
- **action**: What operations, such as deleting and creating, this permission policy allows the collaborators to perform on the **resource**. The operations are usually described using APIs.
- **effect**: Whether this permission policy allows collaborators to perform such operations.

When you have planned the permission settings, you can assign the permissions. The following example shows how to permit collaborators to create an image repository:

1. Create a custom policy (see the [CAM document](https://intl.cloud.tencent.com/document/product/598/10601#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5)).
2. Log in to the Tencent Cloud Console using your developer account.
3. Go to the [CAM custom policy management page](https://console.cloud.tencent.com/cam/policy/custom) and click **Create a custom policy** to open the **Select a policy creation method** dialog box. This is shown in the following figure:
   ![Select the Automatic Adjustment Policy Creation Method](https://main.qcloudimg.com/raw/6866d6a17e7f9f80d17ff8cc5430e821.png)
4. Select **Create by Policy Syntax**>**Blank Template**.
   ![Select Template](https://main.qcloudimg.com/raw/95aae943cf4c870e00fa35eb5c731379.png)
5. Click **Next Step** to enter the **Edit Policy** page.
6. Set the policy name, and enter the following content into the **Edit Policy Content** editing box.

```
        {
            "version": "2.0",
            "statement": [{
                "action": "ccr:CreateRepository",
                "resource": "qcs::ccr:::repo/*",
                "effect": "allow"
            }]
        }
```

 For example, set the policy name to `ccr-policy-demo`, as shown in the following figure:
![](https://main.qcloudimg.com/raw/6ddb62043ab1744ddbbd7ef9963dd838.png)

> At the **end** of "resource", use \* to indicate that an image repository can be created under any namespace.

6. Click **Create Policy** to complete the policy creation process.
   ![](https://main.qcloudimg.com/raw/077b225d89838abc6dfd1925096f7b30.png)
7. Associate a custom policy. After the policy (`ccr-policy-demo`) is created in step 1, you can associate it with any collaborator. For more information, see the [CAM Documentation](https://intl.cloud.tencent.com/document/product/598/10602#.E7.94.A8.E6.88.B7.E5.85.B3.E8.81.94.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5). After the policy has been associated, the collaborators have **create image repository permissions in any namespace**.
   \_resource `qcs::ccr:::repo/*` Format description:

- `qcs::ccr:::` is a fixed format, indicating the developer's TKE image repository service.
- `repo` is a fixed prefix, representing the resource type, which is an image repository here.
- `*` after the slash (`/`) means matching all image repositories.

For a detailed description of resource, see [CAM Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).

#### Authorizing by Resource

You can authorize multiple resources at the same time. For example, **to allow deletion of image repositories in namespace foo and bar**, you can create the following custom policy:

```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository"
        ],
        "resource": [
            "qcs::ccr:::repo/foo/*",
            "qcs::ccr:::repo/bar/*"
        ],
        "effect": "allow"
    }]
}
```

> - `foo/*` in `qcs::ccr:::repo/foo/*` means all images in the image repository namespace `foo`.
> - `bar/*` in `qcs::ccr:::repo/bar/*` means all images in the image repository namespace `bar`.

#### Authorizing by Action (API)

You can configure multiple `actions` for a resource for a centralized management of resource permissions. For example, to **permit the creation, deletion and pushing of image repository in the namespace foo**, you can create the following custom policies:

```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:CreateRepository",
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository",
            "ccr:push"
        ],
        "resource": "qcs::ccr:::repo/foo/*",
        "effect": "allow"
    }]
}
```

## Permission List

#### Docker Client Permissions

resource： `qcs::ccr:::repo/${namespace}/${name}`  
action:

- `ccr:pull`: Use the Docker command line to pull an image
- `ccr:push`: Use the Docker command line to push an image

#### Namespace Permissions

resource: `qcs::ccr:::repo/${namespace}`  
action:

- `ccr:CreateCCRNamespace` Create an image repository namespace
- `ccr:DeleteUserNamespace` Delete an image repository namespace

Function Guide: **TKE** > Left sidebar **Image Repositories** > **My Images** > **Namespaces**.
![Create or delete image repository namespace permissions](https://main.qcloudimg.com/raw/d36011d537ebd09bc3467b1ea5308c52.png)

#### Image Repository Permissions

resurce: `qcs::ccr:::repo/${namespace}/${name}`  
action:

- `ccr:CreateRepository` Create an image repository
- `ccr:DeleteRepository` Delete an image repository
- `ccr:BatchDeleteRepository` Batch delete image repositories
- `ccr:GetUserRepositoryList` View the list of image repositories

Function Guide: **TKE** > Left sidebar **Image Repositories** > **My Images** > **My Images**.
![Image repository permissions](https://main.qcloudimg.com/raw/0e9d36ee49e29d73d930af53bf8ead16.png)

> Note: 
> If you want to prevent a collaborator from deleting certain images, configure multiple actions.
> For example, to prohibit deleting any image repository:

```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository"
        ],
        "resource": "qcs::ccr:::repo/*",
        "effect": "deny"
    }]
}
```

<span id="Tag"></span>

#### Image Tag Permissions

resource: `qcs::ccr:::repo/${namespace}/${name}:${tag}`  
action： `ccr:DeleteTag` Delete image tag permissions

Function Guide: **TKE** > Left sidebar **Image Repositories** > **My Images** > **My Images** > Click an image name > **Image Tag** page.
![Image repository permissions](https://main.qcloudimg.com/raw/f2f0accce0b3ee751e8d15f20e174a68.png)



