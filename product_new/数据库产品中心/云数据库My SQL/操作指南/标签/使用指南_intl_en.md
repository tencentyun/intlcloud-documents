### Overview

A **tag** is a key-value pair provided by Tencent Cloud to identify a resource in the cloud. For more information, see [Tag Overview](http://intl.cloud.tencent.com/document/product/651/13334).
You can manage TencentDB for MySQL resources in a categorized manner by using tags in various dimensions such as business, purpose, and person-in-charge, making it easier to find the right resources. Tags have no semantic meaning for Tencent Cloud and are parsed and matches strictly based on strings. During the course of use, you only need to pay attention to applicable [use limits](http://intl.cloud.tencent.com/document/product/651/13354).
Below is a specific use case to show how a tag is used.

### Case Background
A company owns 10 TencentDB for MySQL instances in Tencent Cloud. Distributed in three departments (ecommerce, gaming, and entertainment), these instances are used to serve internal business lines such as marketing, game A, game B, and post-production. The OPS owners of the three departments are John, Jane, and Harry, respectively.

### Setting a Tag
To facilitate management, the company categorizes its TencentDB for MySQL resources with tags and defines the following tag key-value pairs.

| Tag Key     | Tag Value                             |
| :---------- | ---------------------------------- |
| Department       | Ecommerce, gaming, and entertainment                   |
| Business       | Marketing, game A, game B, and post-production |
| OPS owner | John, Jane, and Harry                   |

These tag keys/values are bound to TencentDB for MySQL instances in the following way:

|instance-id	|Department	|Business	|OPS Owner|
|----------------|-------|----|--------------|
|cdb-abcdef1	|Ecommerce	|Marketing	|Harry|
|cdb-abcdef2	|Ecommerce	|Marketing	|Harry|
|cdb-abcdef3|Gaming|Game A|John|
|cdb-abcdef3|Gaming|Game B|John|
|cdb-abcdef4||Gaming|Game B|John|
|cdb-abcdef5||Gaming|Game B|Jane|
|cdb-abcdef6|Gaming|Game B|Jane|
|cdb-abcdef7|Gaming|Game B|Jane|
|cdb-abcdef8	|Entertainment	|Post-production|	Harry|
|cdb-abcdef9	|Entertainment	|Post-production|	Harry|
|cdb-abcdef10|	Entertainment	|Post-production|	Harry|

### Using a Tag
For more information on how to create and delete a tag, see [Getting Started with Tags](https://intl.cloud.tencent.com/document/product/651/32582).

For more information on how to edit a tag in TencentDB for MySQL, see [Editing a Tag](https://intl.cloud.tencent.com/document/product/236/31918).

