## Overview

You can grant a user the permission to view and use specific resources in the [Game Player Matchmaking (GPM) console](https://console.cloud.tencent.com/gpm) by using CAM policies. The examples below show how to do so.

## Directions

### Full access policy for GPM

To grant a user the permission to create and manage GPM resources, you can include the following operation in your policy, and then associate the policy with the user.

The detailed steps are as follows:
1. Create a custom policy for viewing GPM statistics as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/35596). The example policy syntax is as follows:
```
{
			"version": "2.0",
			"statement": [
				{
					"action": [
						"gpm:*"
					],
					"resource": "*",
					"effect": "allow"
				}
			]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

### Read-only policy for GPM

To grant a user permission to query any GPM resources, but not create, delete, or modify them, you can include the following operation in your policy, and then associate the policy with the user.

The detailed steps are as follows:
1. Create a custom policy for viewing GPM statistics as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/35596). The example policy syntax is as follows:
```
{
			"version": "2.0",
			"statement": [
				{
					"action": [
						"gpm:Describe*",
					],
					"resource": "*",
					"effect": "allow"
				}
			]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

### Rule operation policy in GPM console

To grant a user the permission for rule on GPM, you can include the following operation in your policy, and then associate it with the user.

| API | Description |
| ------------- | ---------------- |
| ModifyRule | Modifies a rule |
| DeleteRule | Deletes a rule |
| DescribeRule | Queries rule details |
| DescribeRules | Queries the rule list and paginates the query results |


The detailed steps are as follows:
1. Create a custom policy for matching on GPM as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/35596). The example policy syntax is as follows:
```
{
			"version": "2.0",
			"statement": [
					{
							"action": [
									"gpm:ModifyRule",
									"gpm:DeleteRule",
									"gpm:DescribeRule",
									"gpm:DescribeRules"
							],
							"resource": "*",
							"effect": "allow"
					}
			]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.


### Matchmaking operation policy in GPM console

To grant a user the permission for creating, modifying, and deleting a match on GPM, you can include the following operation in your policy, and then associate it with the user.

| API | Description |
| --------------- | ---------------- |
| ModifyMatch | Modifies a match |
| DeleteMatch | Deletes a match |
| DescribeMatch  | Queries matchmaking details |
| DescribeMatches | Queries the matchmaking list and paginates the query results |
| DescribeRules | Queries the rule list and paginates the query results |

The detailed steps are as follows:
1. Create a custom policy for matching on GPM as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/35596). The example policy syntax is as follows:
```
{
			"version": "2.0",
			"statement": [
					{
							"action": [
									"gpm:ModifyMatch",
									"gpm:DeleteMatch",
									"gpm:DescribeMatch",
									"gpm:DescribeMatches",
									"gpm:DescribeRules"
							],
							"resource": "*",
							"effect": "allow"
					}
			]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.


### Statistics viewing policy in GPM console


To grant a user the permission to view all matchmaking statistics, you can include the following operations in your policy, and then associate the policy with the user.

| API | Description |
| --------------- | ---------------- |
| DescribeMatches | Queries the matchmaking list and paginates the query results |
| DescribeData | Queries statistics |


The detailed steps are as follows:
1. Create a custom policy for matching on GPM as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/35596). The example policy syntax is as follows:
```
{
			"version": "2.0",
			"statement": [
					{
							"action": [
					"gpm:DescribeMatches",
					"gpm:DescribeData",
					"gpm:DescribeMatchCodes"
							],
							"resource": "*",
							"effect": "allow"
					}
			]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.



### GPM matchmaking usage policy

To grant a user the permission to use the complete features of initiating a match, canceling a match, and querying matchmaking progress for all MatchCodes, you can include the following operations in your policy, and then associate the policy with the user.

| API | Description |
| ------------------------ | ------------ |
| StartMatching | Initiates a match |
| CancelMatching | Cancels a match |
| DescribeMatchingProgress | Queries matchmaking progress |


The detailed steps are as follows:
1. Create a custom policy for matching on GPM as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/35596). The example policy syntax is as follows:
```
{
			"version": "2.0",
			"statement": [
					{
							"action": [
									"gpm:StartMatching",
									"gpm:CancelMatching",
									"gpm:DescribeMatchingProgress"
							],
							"resource": "*",
							"effect": "allow"
					}
			]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.
