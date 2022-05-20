## Overview
By generating a temporary credential for cross-account access, you can enable one of your Tencent Cloud accounts to play the role of another Tencent Cloud account, and manage Tencent Cloud resources within the scope of authority.
## Prerequisite
You already had multiple root accounts. If you want to create one, please refer to [register](https://intl.cloud.tencent.com/document/product/378/17985). Assume that you have two Tencent Cloud accounts, Account A and Account B. You want to manage the resources under Account B by using Account B.
## Directions
1. [Log in](https://intl.cloud.tencent.com/document/product/378/36004) with Account A and create the custom role as instructed in [Creating Role](https://intl.cloud.tencent.com/document/product/598/19381).
2. Use the access key for account B to generate a temporary security key by invoking [sts: AssumeRole](https://intl.cloud.tencent.com/document/product/598/35840) through the Cloud API tool.
3. Use the key generated in Step 2 as account A to invoke the API through the Cloud API tool. In this case, you can manage Tencent Cloud resources.
