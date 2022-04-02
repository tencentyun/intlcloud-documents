
## Overview
Tencent Container Registry (TCR) Enterprise Edition supports protection for the hosted container image tags. Container image security is a key part of cloud-native application delivery. It enables tag immutability feature for the images hosted in TCR, which ensures the images of the same tag will only be successfully pushed once, thus effectively reduce the risk of tag overwriting caused by misoperation in the production environment. TCR supports tag protection at the namespace level. Users can fine-grainly define the repositories and image tags covered by the feature according to service demands.



## Directions

### Creating tag immutability rule

1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Tag Management** > **Tag Immutability** on the left sidebar.
2. Select the region where the instance is located and the instance name on the “Tag Immutability” page.
3. Click **Create Rule**. In the **Create Tag Immutability Rule** window, configure the rule based on the following information. See the figure below:
![](https://main.qcloudimg.com/raw/09be5b8f7ec3ced346236fc2d97f1bff.png)
<table>
<tr><th style="width: 20%">Configuration Item</th><th>Description</th></tr>
</tr>
<tr>
<td>Associated instance</td>
<td>The instance which has been selected currently.</td>
</tr>
<tr>
<td>Namespaces</td>
<td>The current instance needs to enable the namespace for tag protection. Only a rule can be created in a single namespace.</td>
</tr>
<tr>
<td rowspan="2">Immutability rule</td>
<td ><b>latest</b>: in all repositories in the current namespace, all image tags are not allowed to be overwritten except the latest tag.</td>
</tr>
<tr>
<td><b>Custom</b>: customize the configuration of the repository and image tag that need to be matched.<br><ul><li><b>Repository matching</b>: select filter type for the image repository, and enter the name of the repository which needs to be filtered.</li><li><b>Tag matching</b>: select filter type for the image tag, and enter the name of the tag which needs to be filtered.</li></ul></td>
</tr>
<tr>
<td>Rule switch</td>
<td>The rule is effective as of creation by default.
<dx-alert infotype="notice" title="">
Enabling means the rule takes effect. You can enable/disable the rule in the configuration.
</dx-alert>
</td>
</tr>
</table>

4. Click **Confirm** to create the rule.



### Managing tag immutability rule
You can view the rules on the “Tag Immutability” page after creation, and take the following actions to manage the rules.
- **Configuration**: you can reconfigure the instance tag immutability rule but cannot modify the namespace for which it takes effect.
- **Delete**: delete the tag immutability rule under the instance.

