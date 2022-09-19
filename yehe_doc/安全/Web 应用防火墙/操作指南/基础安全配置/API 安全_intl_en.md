This document describes how to add APIs or API rule files using the API security feature to protect your APIs.
## Overview
Using API security, you can add APIs or API rule files, so that WAF will run security checks on the API requests and allow the APIs that meet specified requirements. This module provides protection for APIs by cooperating with the [AI engine](https://console.cloud.tencent.com/guanjia/tea-baseconfig) and [bot traffic management](https://console.cloud.tencent.com/guanjia/tea-botconfig) modules.
>! AI security is a beta feature, which is currently free of charge and will begin charging at the list price after it is released officially.

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the page displayed, select a target domain name in the upper-left corner, and click **API security**.
3. On the API security page, you can add API security rules by either [importing APIs](#import) or [adding APIs](#add). 
>?
>- Import API (recommended): You need to import an API file that meet the specified requirements.
>- Add API: You need to add the API path of a website manually.

[](id:import)
### Importing APIs (recommended)
1. Select **Basic Security** > **API security**. On the page that appears, click **Import API**.
2. In the pop-up window, select a file to upload, and click **Upload**.

>? WAF provides support for parsing swagger2.0 files in YML and JSON formats. The file to import should satisfy the following requirements:
>- Format: The API description file must be suffixed with .yml or .json. The file size cannot exceed 100 KB.
>- Count: Up to 20 APIs can be imported at a time. APIs that already exist will not be imported again.
>- The imported APIs can be reviewed and edited.

![](https://qcloudimg.tencent-cloud.cn/raw/8750b11438d804f42dbda69bd36d5021.png)

3. After the upload, the API security module will parse the API policies in the swagger2.0 file. Then click **OK** when the parsing is complete.
![](https://qcloudimg.tencent-cloud.cn/raw/319bf90f1a5feb0cf6972f272f951f3e.png)

4. You can check the API rules after they are successfully imported.

[](id:add)
### Adding APIs
1. Select **Basic Security** > **API security**. On the page that appears, click **Add rule**.
2. In the pop-up window, create an API security rule that suits your website needs, and click **Add**.
![](https://qcloudimg.tencent-cloud.cn/raw/cc74e4deade2ea3843053103ee895fce.png)

 **Field description:**
  - **API name**: Enter an API path that starts with "/", which cannot be the same as "API name + Request method" in the setting (eg., `/guanjia/waf/config`).
  - **Description**: Enter a description of the API rule. This field is optional.
  - **Enable API**: The switch controls whether to enable an API rule. The switch is off by default. When it is on, the API rule will be parsed and the action (Observe/Block) configured will be performed.
  - **Request method**: Only the following request methods are supported: GET, POST, PUT, and DELETE.
  - **Condition**: You need to specify the following parameters: Parameter name, Parameter location (Only `body`, `query`, and `path` values are supported), Parameter type, Required (If it is ticked, WAF will check whether the parameter is contained in the request and block the parameter when it exists), and Remarks (optional field).
  - **Action**: Select the Observe or Block action as needed.

>? You are encouraged to set the Observe action, which allows the AI security module to check whether false positives occur in attack logs. If no false positives are caused, then change to the Block action.

3. After the rule is added, the API is added to the API security configuration list.
![](https://qcloudimg.tencent-cloud.cn/raw/f39ffaad472e01d02675369d79b55ad9.png)

**Field description:**
  - **Rule ID**: It is a unique identifier for an API rule and is created automatically after the rule is added. You can search logs of the rule by its ID in [Attack Logs](https://console.cloud.tencent.com/guanjia/tea-attacklog).
  - **API name (description)**: It displays the configured API name and description. Note that the API name must be the actual path of the API.
  - **Source**: It displays whether an API is parsed from file or added manually.
  - **Request method**: The following request methods are supported: GET, POST, PUT, and DELETE.
  - **API parameter**: List of API parameters configured, which cannot exceed 30.
  - **Action**: It can be set to Observe or Block.
  - **On/Off**: The switch controls whether to enable an API rule. To enable or disable multiple switches at the same time, select multiple API rules and click **Batch enable** or **Batch disable**.
  - **Last modified**: The last time an API rule is modified.
  - **Operation**: It allows you to edit or delete an API rule. If you want to delete API rules in batches, you can select more than one rule and click **Batch delete**.
