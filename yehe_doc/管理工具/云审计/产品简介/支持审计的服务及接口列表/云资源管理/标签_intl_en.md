As the number of Tencent Cloud user resources grows, user resource management becomes more and more difficult. To help you query and manage various resources more quickly and efficiently, Tencent Cloud provides the Tag service, which allows you to manage existing Tencent Cloud resources by category and schedule them with preset tags. Tags are words and phrases serving as metadata used to identify and organize Tencent Cloud resources. The tag limit varies by resource type, and most resources can have up to 50 tags.

Tag operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|--------------------|------|------------------------------|
| Associating tag with resource             | tag  | AddResourceTag               |
| Creating tag               | tag  | CreateTag                    |
| Deleting resource tag             | tag  | DeleteResourceTag            |
| Deleting tag               | tag  | DeleteTag                    |
| Querying the list of businesses connected to Tag Console           | tag  | GetResourceMenu              |
| Querying resource list through tag         | tag  | GetResourcesByTags           |
| Querying resource tag             | tag  | GetResourceTags              |
| Querying all tag keys and values of resource       | tag  | GetResourceTagsByResourceIds |
| Querying tag key              | tag  | GetTagKeys                   |
| Querying tag list             | tag  | GetTags                      |
| Querying tag value              | tag  | GetTagValues                 |
| Manipulating (adding, updating, or deleting) all resource tags in batches | tag  | ModifyResourceTags           |
| Modifying resource tag value            | tag  | UpdateResourceTagValue       |
