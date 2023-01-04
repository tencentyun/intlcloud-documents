A tag is a key-value pair provided by Tencent Cloud and can be used to easily identify resource. For more information, see [Tag Overview](https://intl.cloud.tencent.com/document/product/651/13334).

You can use tags to categorize and manage TDSQL-C for MySQL resources in various dimensions such as business, purpose, and person-in-charge, so you can find the target resources quickly. Tags have no semantic meaning in Tencent Cloud. They are parsed and matched strictly based on strings. When using tags, you need to pay attention to the [use limits](https://intl.cloud.tencent.com/document/product/651/13354).

The following example shows how a tag is used.

## Example
**Background**
A company has 5 TDSQL-C for MySQL clusters in Tencent Cloud, which are owned by three departments: Ecommerce, Game, and Entertainment. The clusters are used for services such as marketing, gaming, and post-production. The Ops owners of the three departments are John, Jane, and Harry, respectively.
**Setting a tag**
For more efficient management, the company uses tags to categorize the database resources, and defines the following tag key-value pairs:

| Tag Key | Tag Value | 
|---------|---------|
| Department | Ecommerce, Game, and Entertainment |
| Business | Marketing, Gaming, and Post-production|
| Ops owner | John, Jane, and Harry |

Then bind the above tag key-value pairs to TDSQL-C for MySQL. The relationship between resources and the tag key-value pairs is shown in the table below.

| instance-id | Department | Service | Ops owner |
|---------|---------|---------|---------|
| ceshi-abc1 | Ecommerce | Marketing | John |
| ceshi-abc2 | Game | Gaming | Jane |
| ceshi-abc3 | Game | Gaming | Jane |
| ceshi-abc4 | Entertainment | Post-production | Harry |
| ceshi-abc5 | Entertainment | Post-production | Harry |

## Related Operations
- [Creating Tag for Cluster](https://www.tencentcloud.com/document/product/1098/50150)
- [Editing and Deleting Tag](https://www.tencentcloud.com/document/product/1098/50149)
