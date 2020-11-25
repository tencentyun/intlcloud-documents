### Introduction
**Tags** are key-value pairs provided by Tencent Cloud to easily identify resource. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/651/13334).
You can use tags to categorize and manage TencentDB for PostgreSQL resources by various metrics such as business, purpose, and owner. You can also quickly locate a resource by its tag. In Tencent Cloud, the tag key-value pairs have no semantic meaning and are strictly parsed and matched as strings. To use tags, please pay attention to [use limits](https://intl.cloud.tencent.com/document/product/651/13354) first.
Here we describe a use case to show how a tag is used.

### Use Case Background
A company has three PostgreSQL instances in Tencent Cloud. Those instances are distributed in three gaming businesses whose OPS owners are John, Jane, and Harry.

### Configuring Tags
To manage the resources better, the company categorizes its TencentDB for PostgreSQL resources with tags and defines the following tag key-value pairs.

| Tag Key     | Tag Value                             |
| :--------- | ------------------- |
| Business | Game 1, game 2, and game 3 |
| OPS owner | John, Jane, and Harry                   |

These tag key-value pairs are bound to TencentDB for PostgreSQL instances in the following way:

| instance-id      | Business  | OPS Owner |
| ---------------- | ----- | ---------- |
| postgres-abcdef1 | Game 1 | Harry       |
| postgres-abcdef2 | Game 2 | Jane       |
| postgres-abcdef3 | Game 3 | John       |

### Using Tags
For more information on how to create and delete a tag, please see [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).

For more information on how to edit a tag in TencentDB for PostgreSQL, please see [Editing a Tag](https://intl.cloud.tencent.com/document/product/409/38840).
