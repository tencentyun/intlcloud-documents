
## Issue
The subnet cannot be selected during CCN access.

## Possible Causes
The account of the CCN-associated VPC is different from that running the migration/sync task.

## Solutions
The account of the CCN-associated VPC must be the same as that running the migration/sync task.

For example, to migrate an instance from account A to account B, you should use account B to create a task, so the CCN-associated VPC must be under account B.

For more information on CCN configuration, see [CCN Access: Configuring VPC-IDC Interconnection Through CCN](https://intl.cloud.tencent.com/document/product/571/42650).

