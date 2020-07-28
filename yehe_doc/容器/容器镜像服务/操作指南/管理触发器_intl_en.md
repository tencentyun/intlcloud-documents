## Scenario

Tencent Container Registry (TCR) allows users to configure and use the flexible trigger feature. By configuring appropriate triggers in instances to quickly access the existing R&D process and CI/CD platform, users can realize container DevOps scenarios such as automatic triggering of application deployment by image update.

The trigger feature allows users to create custom trigger rules and view triggering logs. Triggering actions support the push, pull, and deletion of container images and Helm Chart. Trigger rules support flexible filtering by regular expressions. They also support regular filtering rules by specifying namespaces in instances and configuring image repositories and tags. In this way, the feature allows triggers to be launched only by certain repositories or image tags in special naming formats. The Header customization feature supports the configuration of the Header in `Key:Value` format for accessing the destination URL, which can be applied to authentication and other scenarios.


## Prerequisites

Before creating and managing a trigger in a TCR Enterprise Edition instance, complete the following preparations:
- You have [created an TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, ensure that you have granted the sub-account operation permissions for the corresponding instance in advance. For more information on how to grant the permissions, see [Examples of TCR Enterprise Edition Authorization Schemes](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating a trigger
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Trigger** in the left sidebar.
On the "Trigger" page, you can view the list of trigger rules for the current instance. To change the instance, at the top of the page, select the desired instance name from the "Instance Name" drop-down list.
2. Click **Create**. In the "Create a Trigger" window that appears, configure the rule by referring to the following field description.
![](https://main.qcloudimg.com/raw/efe4881f8a427899c8c73258e0cfbc4a.png)
 - **Name**: indicates the instance rule name. It supports lowercase letters, numbers, and three symbols (`-`, `.`, and `_`) and must start with a letter. In this document, `webhook-demo` is the sample instance rule name.
 - **Description**: indicates the rule description.
 - **Triggering action**: currently, six options are available: image push, image pull, image deletion, Helm Chart upload, Helm Chart download, and Helm Chart deletion. During the execution of a trigger, the webhook request initiated will contain information about the triggering action.
 - **Triggering rules**:
    - **Triggering instance**: indicates the instance to which the trigger belongs, that is, the current selected instance. This field cannot be modified.
    - **Namespace**: indicates the namespace where the trigger runs. If the list is empty, first [create a namespace](https://intl.cloud.tencent.com/document/product/1051/35487) in the instance.
    - **Repository name**: indicates the name of the repository where the trigger runs. Regex matching of the image repository and Helm Chart repository is supported.
>? Regex rules can be specified as `nginx-*` and `{repo1，repo2}`, in which:
> - `*` : matches any field that does not contain '/'.
> - `**`: matches any field that contains '/'.
> - `?`: matches any single non-'/' character.
> - `{option 1,option 2,...}`: matches multiple options simultaneously.
>
    - **Tag**: indicates the tag for which the trigger runs. Regex matching is supported. The rule is the same as the repository name rule. To apply the trigger to all tags, leave this parameter unspecified.
 - **URL**: indicates the destination URL for the request initiated after the trigger is fired. The trigger will initiate a POST request to the URL, and the request body will contain information such as the triggering action and trigger rule.
 - **Header**: indicates the Header information that can be carried when the trigger initiates a POST request. It supports the Key:Value format, such as `Authentication: xxxxxxx`.
3. Click **OK** to create the synchronization rule.

### Managing trigger rules
After trigger rules are created, you can view created trigger rules on the "Trigger" page. You can perform the following operations to manage trigger rules, as shown in the following figure:
![](https://main.qcloudimg.com/raw/fd3501d656bcc695e1c1f4219404ae6d.png)
- **View triggering logs**: you can click the name of a trigger rule to view its triggering log. For more information, see [Viewing trigger logs](#CheckLog).
- **Modify rule status**: <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px"> indicates that the rule is enabled. <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> indicates that the rule is disabled. New instance synchronization rules are enabled by default. You can adjust them based on your requirements.
- **Configure**: is to re-configure the trigger rule. You can re-configure all parameters.
- **Delete**: is to delete the trigger rule.

<span id="CheckLog"></span>
### Viewing triggering logs
You can click the name of a trigger rule to view its triggering log, as shown in the following figure:
![](https://main.qcloudimg.com/raw/ffd9525f3ef89e02d38cce808fc6bcd8.png)
The log contains the following information:
- **Task ID**: indicates the ID of the trigger task, which is unique in the instance.
- **Triggering action**: indicates the action that fires this trigger, for example, image push.
- **Triggering repository**: indicates the repository that generates this triggering action.
- **Status**: indicates the status when the trigger successfully executes the webhook request.
- **Creation time**: indicates the time when the trigger is launched, that is, when the webhook request is initiated.

## Related Information
### Webhook request format reference
When users perform an action on resources that meet the rule, for example, pushing a new image to the specified image repository, the corresponding trigger will be fired, and an HTTP POST request will be initiated to the URL configured in the rule. The request body contains information such as the triggering action and repository path. The following request body information is parsed after the triggerring by an image push action. This information can be used as a reference for developing the Webhook server.
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
