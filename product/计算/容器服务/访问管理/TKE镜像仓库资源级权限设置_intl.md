## Overview of the TKE Image Service Permissions

To describe the TKE image, use the following format: `ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}`.
The following fields are required for configuring the permissions of Image Registry :
- `${namespace}`: The namespace to which the image belongs.
- `${name}`: Image name.

>! Do not add slashes (/) to the namespace `${namespace}` and the image name `${name}`. 
> The `${tag}` field currently is only for authenticating the permissions for deleting.  For more information, see [Image Tag Permissions](#¾µÏñTagÈ¨ÏÞ).

 `${namespace}` and `${name}` fields allow you to develop detailed permission schemes for collaborators to flexibly manage access permissions.  
For example:
* Allowing collaborator A to pull an image
* Preventing collaborator A deleting an image
* Preventing collaborator B  pulling an image from namespace ns1

If you do not need to manage your Image Registry permissions precisely, you can use the [preset policy authorization](#Ô¤Éè²ßÂÔÊÚÈ¨).
Otherwise, use the [custom policy authorization](#×Ô¶¨Òå²ßÂÔÊÚÈ¨).
The TKE image service utilizes CAM (Cloud Access Management) to manage access permissions.  You can learn more about how to use CAM here:
- [User management](https://cloud.tencent.com/document/product/598/17289)
- [Policy management](https://cloud.tencent.com/document/product/598/10601)
- [Authorization management](https://cloud.tencent.com/document/product/598/10602)

## Preset Policy Authorization

To simplify TKE image service permission management, the TKE image service has two preset policies:
* [Image Registry full read/write permission](https://console.cloud.tencent.com/cam/policy/detail/419082&QcloudCCRFullAccess&2)
This preset policy configures all permissions of the TKE image service. After a collaborator is associated with this policy, they will have the same Image Registry permissions as the developer. For details, see the [permission list](#È¨ÏÞÁÐ±í).
* [Image Registry read-only permission](https://console.cloud.tencent.com/cam/policy/detail/419084&QcloudCCRReadOnlyAccess&2)
This preset policy includes only the read-only permission for the TKE image service. If a collaborator is **only** associated with this policy in the TKE image service, the following operations will be prohibited:
 - Pushing an image using `docker push`
 - Creating an Image Registry namespace
 - Deleting an Image Registry namespace
 - Creating an image repository
 - Deleting an image repository
 - Deleting an image tag

If you don't know how to associate a preset policy with a collaborator, see the following CAM documents: [Preset Policy Overview](https://cloud.tencent.com/document/product/598/10601#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5) and [Associating a User with a Preset Policy](https://cloud.tencent.com/document/product/598/10602#.E9.A2.84.E8.AE.BE.E7.AD.96.E7.95.A5.E5.85.B3.E8.81.94.E7.94.A8.E6.88.B7).

## Custom Policy Authorization

With a custom policy, you can associate different permissions with different collaborators.
Taking the following factors into account when assigning permissions:
- **resource**: Which images are associated with this permission policy, for example, all image repositories are described as `qcs::ccr:::repo/*`. For more information, see [CAM Resource Description Method](https://cloud.tencent.com/document/product/598/10606);
- **action**: The operations, such as deleting and creating, this permission policy allows the collaborators to perform on the **resource**. The operations are usually described using APIs;
- **effect**: Whether this permission policy allows the collaborators to perform such operations.

Now you can begin assigning permissions. The example below describes "how to grant a collaborator to create an image repository":
1. Create a custom policy (see the [CAM document](https://cloud.tencent.com/document/product/598/10601#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5)).
  - Log in to the Tencent Cloud console using your developer account.
  - Go to the [CAM custom policy management page](https://console.cloud.tencent.com/cam/policy/custom) and click "Create a custom policy" to open the "Select a policy creation method" dialog box.
![Select a policy creation method][6]
 - Select "Create by policy syntax" > "Blank template".
![Select a template][7]
 - Click "Next" at the bottom of the page to go to the "Create by policy syntax" > "Edit policy" page.
 - Enter the following in the "Edit policy content" edit box and enter a meaningful name in "Policy name", such as `ccr-policy-demo`.
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
    ![Edit policy][8]
>? At the **end** of "resource", use \* to indicate that an image repository can be created under any namespace.
 - Click "Create a policy" at the bottom of the page to complete the policy creation process.
![Edit policy][9]
2. Associate a custom policy. After the policy (`ccr-policy-demo`) is created in step 1, you can associate it with any collaborator. For more information, see the [CAM document](https://cloud.tencent.com/document/product/598/10602#.E7.94.A8.E6.88.B7.E5.85.B3.E8.81.94.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5). After the policy is associated, the collaborator has the **permission to create an image repository in any namespace**.
_resource `qcs::ccr:::repo/*` Format description:
 - `qcs::ccr:::` is a fixed format, indicating the developer's TKE Image Registry service.
 - `repo` is a fixed prefix, representing the resource type, which is an image repository here.
 - `*` after the slash (`/`) means matching all image repositories.

For a detailed description of the resource, see [CAM Resource Description Method](https://cloud.tencent.com/document/product/598/10606).

#### Authorizing by Resource

You can authorize multiple resources at the same time. For example, "to allow deleting image repositories in namespace foo and bar", you can create a custom policy as follows:
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

>!
> - `foo/*` in `qcs::ccr:::repo/foo/*` means all images in the image repository namespace `foo`.
> - `bar/*` in `qcs::ccr:::repo/bar/*` means all images in the image repository namespace `bar`.

#### Authorizing by Action (API)

You can configure multiple `actions` for one resource to manage permission more easily. For example, "to allow creating, deleting, and pushing image repositories in namespace foo", you can create the following custom policy:
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

resource£º `qcs::ccr:::repo/${namespace}/${name}`  
action:
- `ccr:pull`: Use the docker command line to pull an image
- `ccr:push`: Use the docker command line to push an image

#### Namespace Permissions

resource: `qcs::ccr:::repo/${namespace}`  
action:
- `ccr:CreateCCRNamespace`     Create an image repository namespace
- `ccr:DeleteUserNamespace`    Delete an image repository namespace

Feature guide: **TKE** > **Image Registry** in the left sidebar > **My images** > **Namespaces**
![Permissions for creating or deleting image repository namespace][1]


#### Image Registry Permissions

resurce: `qcs::ccr:::repo/${namespace}/${name}`  
action:
- `ccr:CreateRepository`        Create an image repository
- `ccr:DeleteRepository`        Delete an image repository
- `ccr:BatchDeleteRepository`   Batch delete image repositories
- `ccr:GetUserRepositoryList`  View the list of image repositories

Feature guide: **TKE** > **Image Registry** in the left sidebar > **My images** > **My creations**
![Image repository permission][4]

>! To prevent a collaborator from deleting certain images, configure multiple actions.
>
For example. to prohibit deleting any image repository:
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

#### Image Tag Permissions

resource: `qcs::ccr:::repo/${namespace}/${name}:${tag}`  
action:
 `ccr:DeleteTag` Permission to delete an image tag

Feature guide: **TKE** > **Image Registry** in the left sidebar > **My images** > **My creations** > click an image name > **Image tag** page
![Image repository permission][5]



[1]:https://mc.qcloudimg.com/static/img/1be5647f80dcc50db26cf13ef0e29ce5/1.png
[2]:https://mc.qcloudimg.com/static/img/aec6771c2595210d3e4319e6188aafa9/2.png
[3]:https://mc.qcloudimg.com/static/img/1d7f13366192079ea3c64d70e46f5215/3.png
[4]:https://mc.qcloudimg.com/static/img/99a097e254a9e0e13839d8eaff7b26a8/4.png
[5]:https://mc.qcloudimg.com/static/img/3efec02b8ade10fa5c7778820ebdfec3/6.png
[6]:https://mc.qcloudimg.com/static/img/224dd2cc5dc809c3220d50ba6497a36e/5.png
[7]:https://mc.qcloudimg.com/static/img/daf81fe58cac20aa2c27c65a776288fa/7.png
[8]:https://mc.qcloudimg.com/static/img/fb69dccc77754060b713361034acac18/8.png
[9]:https://mc.qcloudimg.com/static/img/1492b89bdb394490ab5613a1e06b8987/9.png

