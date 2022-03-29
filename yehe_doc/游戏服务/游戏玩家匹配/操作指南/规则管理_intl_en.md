>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31 , 2022.

This document describes how to manage rules through console.

## Prerequisites
Your application for free trial has been approved in [GPM console](https://console.cloud.tencent.com/gpm). For more information, see [ Getting Started](https://intl.cloud.tencent.com/document/product/1072/39200).

## Directions
### Creating a rule
1. Log in to the [GPM console](https://console.cloud.tencent.com/gpm) and click **Rules** on the left sidebar.
2. On the **Rules** page, click **Create**.
![](https://main.qcloudimg.com/raw/042efc9b905fc04536a38d0e751928f7.jpg)

3. Enter the rule name, description, and rule script. Click **Validate** to validate the rule.
![](https://main.qcloudimg.com/raw/eea71ddf1090dae3990745a22988feb5.jpg)
 - Name: enter the rule name (required). It can contain up to 128 bytes.
 - Description: the description of the rule (optional). It can contain up to 1024 bytes.
 - Rule Script: required. It can contain up to 65535 bytes. For the syntax of the rule script, please see [Rule Script Design Guide](https://intl.cloud.tencent.com/document/product/1072/39869).

4. Click **OK**. After a rule is created, its corresponding RuleCode will be generated on the**Rules** page.
![](https://main.qcloudimg.com/raw/60e5ff0061efa06c64d1eaea89998c1d.jpg)

### Viewing a rule
On the **Rules** page, click the RuleCode of a rule to view its details.
![](https://main.qcloudimg.com/raw/bb9bddeda1fcc10f82a7da6e12712e41.jpg)

### Editing a rule
![](https://main.qcloudimg.com/raw/7603d7caf67cd8f6875bcacfb6830735.jpg)
On the details page, you can edit the rule name and description. Once a rule is created, the rule script cannot be edited. You can clone the rule, and redesign the rule script in the new rule.

### Cloning a rule
On the **Rules** page, select a rule in the rule list and click **Clone** in the **Operation** column to create a rule.
![](https://main.qcloudimg.com/raw/57882f396537016cc31a47a663a844e6.jpg)

### Deleting a rule
On the **Rules** page, select a rule in the rule list and click **Delete** in the **Operation** column to create a rule that has not associated with a match.
>!Once deleted, the rule cannot be restored. If you want to delete the rule that is being associated with a match, you can modify the matchmaking information first to disassociate the match from the rule.
>
![](https://main.qcloudimg.com/raw/e88d043965ac7ec0d2a631da8925be53.jpg)



