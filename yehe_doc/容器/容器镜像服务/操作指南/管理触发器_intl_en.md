## Overview

Tencent Container Registry (TCR) allows users to configure and use the flexible trigger feature. By configuring a proper trigger in an instance, you can quickly integrate existing R&D processes and CI/CD platforms and realize container DevOps scenarios such as image updates automatically triggering application deployment.

The trigger feature allows users to create custom trigger rules and view triggering logs. Trigger actions support the push, pull, and deletion of container images and Helm Charts. Triggering rules support flexible regular expression filtering and regular filtering based on specified namespaces in an instance and configured image repositories and tags. This allows the trigger to be triggered by only certain repositories or image tags that use special naming formats. The custom Header feature allows users to configure the Header for accessing the target URL in the `Key:Value` format, which is applicable to authentication and other scenarios.


## Prerequisites

Before creating and managing a trigger in an TCR Enterprise Edition instance, complete the following tasks:
- You have [purchased an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating a trigger
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Trigger** in the left sidebar.
On the "Trigger" page, you can view the list of trigger rules for the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
2. Click **Create**. In the "Create a Trigger" window, configure the rule based on the following information. See the figure below.
![](https://main.qcloudimg.com/raw/70e694eb396edf97d548fd300307bb81.png)

 - **Name**: instance rule name. It supports lowercase letters, numbers, and three symbols (`-`, `.`, and `_`). It must start with a letter or number. In this document, `webhook-demo` is used as an example.
 - **Description**: rule description.
 - **Action**: currently, four trigger actions are supported: push image, delete image, upload Chart, and delete Chart. During the trigger execution, the initiated webhook request will contain information about the trigger action.
 - **Triggering Rule**:
    - **Triggered Instance**: the instance to which the trigger belongs, which is the currently selected instance and cannot be changed.
    - **Namespace**: the namespace for which the trigger takes effect. If the list is empty, please first [create namespaces](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
    - **Repository Name**: the name of the repository for which the trigger takes effect. [Regular matching](https://intl.cloud.tencent.com/document/product/1051/35488) of image repositories and Helm Charts is supported.
    - **Tag**: the tag for which the trigger takes effect. It supports [regular matching](https://intl.cloud.tencent.com/document/product/1051/35488). If you want the trigger to take effect for all tags, you can leave this parameter empty.
 - **URL**: the target URL for request initiation after the trigger is triggered. The trigger will send a POST request to the URL, and the request body contains the trigger action, triggering rule, and other information.
 - **Header**: the Header information in Key:Value format to be carried in a POST request initiated by the trigger, for example, `Authentication: xxxxxxx`.
3. Click **Confirm**.

### Managing trigger rules
After a trigger rule is created, you can view the trigger rule on the "Trigger" page. Then, you can perform the following operations to manage trigger rules. See the figure below:
![](https://main.qcloudimg.com/raw/408ac4c6409ae1f24f8a90c8652120bc.png)

- **View Triggering Log**: you can click the name of a specific trigger rule or click **Triggering Logs** to the right of the trigger rule name to view the triggering log of the rule. For more information, see [Viewing Trigger Logs](#CheckLog).
- **Modify Rule Status**: <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px"> indicates that a rule is enabled, and <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> indicates that a rule is disabled. A newly created trigger rule is enabled by default, and you can change its status as needed.
- **Configuration**: you can re-configure all parameters of the trigger rule.
- **Delete**: you can delete the trigger rule.


### Viewing trigger logs[](id:CheckLog)
You can click the name of a specific trigger rule or click **Triggering Logs** to the right of the trigger rule name to view the triggering log of the rule. See the figure below:
![](https://main.qcloudimg.com/raw/71ffa1471545e6bd8ceb57222fa396ed.png)

The log contains the following information:
- **Task ID**: trigger task ID, which is unique in the instance.
- **Action**: the action that launched the trigger, such as image push.
- **Triggered Repository**: the repository resources that launched the trigger.
- **Status**: success status of the trigger in executing the webhook request.
- **Creation Time**: the time when the trigger was launched, that is, the time when the webhook request was initiated.

## Relevant Information
### Webhook request format for reference
When users perform a relevant action on resources that meet a trigger rule, for example, pushing new images to the specified image repository, the relevant trigger is triggered and sends an HTTP POST request to the URL configured in the rule. The request body contains information such as the trigger action and repository path. The following is the resolved information of a sample request body after the trigger is triggered by image pushing. This sample is for reference in Webhook server development.
```
{
  "type": "pushImage",
  "occur_at": 1589106605,
  "event_data": {
    "resources": [
      {
        "digest": "sha256:89a42c3ba15f09a3fbe39856bddacdf9e94cd03df7403cad4fc105xxxx268fc9",
        "tag": "v1.10.0",
        "resource_url": "xxx-bj.tencentcloudcr.com/public/nginx:v1.10.0"
      }
    ],
    "repository": {
      "date_created": 1587119137,
      "name": "nginx",
      "namespace": "public",
      "repo_full_name": "public/nginx",
      "repo_type": "public"
    }
  },
  "operator": "332133xxxx"
}
```





