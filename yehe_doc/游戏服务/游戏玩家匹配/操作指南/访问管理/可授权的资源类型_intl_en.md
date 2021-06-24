
Resource-level permissions refer to the ability to specify which resources users are allowed to perform operations on. GPM supports resource-level permissions, which means that for certain GPM operations, you can control when users are allowed to perform them, or which specific resources that users are allowed to use. The following will describe the types of resources for which GPM allows permissions.

>! Resource-level permissions specify which resources users can operate on.

Cloud Access Management (CAM) allows you to grant access permissions to the following resources

| Resource Type | Resource Description Method in Access Policies |
| :---------------------------- | ------------------------------------- |
| [Matchmaking](#matchCorrelation) | ` qcs::gpm:$region:$account:match/* ` |
| [Rule](#ruleCorrelation)  | `qcs::gpm:$region:$account:rule/*` |

[Matchmaking APIs](#matchCorrelation) and [Rule APIs](#ruleCorrelation) sections in this document describe GPM API operations that currently support resource-level permissions. When configuring the resource path, you need to replace values of the parameters such as `$region` and `$account` with your actual values. You can also use the wildcard `/*` in the path. For more information, please see [Console Example](https://intl.cloud.tencent.com/document/product/213/10312).
>! GPM API operations not listed in the table do not support resource-level permissions. You can still authorize a user to perform these operations, but you must specify `/*` as the resource element in the policy statement.

<span id="matchCorrelation"></span>

### Matchmaking APIs

| API | Resource Path | Description |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--------------- |
| [StartMatching](https://intl.cloud.tencent.com/document/product/1072/39904) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Initiates a match |
| [CancelMatching](https://intl.cloud.tencent.com/document/product/1072/39908) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Cancels a match |
| [DescribeMatchingProgress](https://intl.cloud.tencent.com/document/product/1072/39907) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Queries matchmaking progress |
| [ModifyMatch](https://intl.cloud.tencent.com/document/product/1072/39929) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Modifies a match |
| [DeleteMatch](https://intl.cloud.tencent.com/document/product/1072/39937) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Deletes a match |
| [DescribeMatch](https://intl.cloud.tencent.com/document/product/1072/39934) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Queries matchmaking details |
| [DescribeMatches](https://intl.cloud.tencent.com/document/product/1072/39932) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Queries the matchmaking list and paginates the results |
| [DescribeData](https://intl.cloud.tencent.com/document/product/1072/39935) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Viewing matchmaking statistics |
| [DescribeMatchCodes](https://intl.cloud.tencent.com/document/product/1072/39933) | `qcs::gpm:$region:$account:match/*`<br>`qcs::gpm:$region:$account:match/$MatchCode` | Queries MatchCode and paginates the results |


<span id="ruleCorrelation"></span>

### Rule APIs

| API | Resource Path | Description |
| :------------ | :----------------------------------------------------------- | :--------------- |
| [ModifyRule](https://intl.cloud.tencent.com/document/product/1072/39928) | `qcs::gpm:$region:$account:rule/*`<br>`qcs::gpm:$region:$account:rule/$RuleCode` | Modifies a rule |
| [DeleteRule](https://intl.cloud.tencent.com/document/product/1072/39936) | `qcs::gpm:$region:$account:rule/*`<br>`qcs::gpm:$region:$account:rule/$RuleCode` | Deletes a rule |
| [DescribeRule](https://intl.cloud.tencent.com/document/product/1072/39931) | `qcs::gpm:$region:$account:rule/*`<br>`qcs::gpm:$region:$account:rule/$RuleCode` | Queries rule details |
| [DescribeRules](https://intl.cloud.tencent.com/document/product/1072/39930) | `qcs::gpm:$region:$account:rule/*`<br>`qcs::gpm:$region:$account:rule/$RuleCode` | Queries rule set list and paginates the results |





