This document describes the features that the Tencent Cloud Tag service provides.
## Managing Resources
The Tag service allows you to tag your resources on Tencent Cloud. You can define tag keys and tag values for resources based on your business needs to implement the classification management of resources. You can query resources based on their regions, types, instances, tag keys, and tag values. The queried resources are displayed in a list. In addition, you can add tags to or delete tags from resources based on your business needs.
## Granting operation permissions on resources by tag
You can customize a tag policy to grant operation permissions on your resources to sub-users or user groups by tag. Based on the tag policy, sub-users or user groups are authorized to perform specified operations on the resources under the specified tags.
## Generating bills by tag
You can generate bills for the costs of your resource usage based on specified tags. These tags are called cost allocation tags. Tags consist of tag keys and tag values. A tag key can have one or more tag values.
● Each tag key that is specified as a cost allocation tag is displayed as an additional column in your bill. The value of a tag key column in each row of a bill is the same as the tag value that you set for the corresponding resource under the tag key. You can also use cost allocation tags to filter and break down bills.
● Tag keys that are not specified as cost allocation tags are not displayed your bill.
For more information, please see [Cost Allocation Tags](https://intl.cloud.tencent.com/document/product/555/32276).
