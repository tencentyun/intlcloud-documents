### Overview

A tag is a key-value pair provided by Tencent Cloud to identify a resource in the cloud.
You can use tags to classify TMP resources based on various factors such as service, usage, and owner. With tags, you can quickly sift through the resource pool and find the corresponding resources. The values of tag keys do not mean anything to Tencent Cloud semantically and will be parsed and matched strictly according to the string. Tencent Cloud will not use your set tags, which are used only for resource management.

Below is a specific use case to show how a tag is used.

### Use Case Background

A company owns 10 TMP instances in Tencent Cloud. Distributed in three departments (ecommerce, gaming, and entertainment), these instances are used to serve internal business lines such as marketing, game A, game B, and post-production. The OPS owners of the three departments are John, Jane, and Harry, respectively.

### Setting Tag

To facilitate management, the company categorizes its TMP resources with tags and defines the following tag key-value pairs:

| Tag Key | 	Tag Value |
|----------|----------|
| Department	| Ecommerce, gaming, and entertainment |
| Business |	Marketing, game A, game B, and post-production |
| OPS owner	| John, Jane, and Harry |

These tags are bound to TMP instances in the following way:

| Instance ID	|Department	|Business	|OPS Owner|
|---|-------|--------|---------|
|   prom-1jqwv1	| Ecommerce	| Marketing	| Harry |
|   prom-1jqwv12	| Ecommerce	| Marketing	| Harry |
|   prom-1jqwv13	| Gaming 	| Game A	| John |
|   prom-1jqwv13	| Gaming 	| Game B	| John |
|   prom-1jqwv14	| Gaming 	| Game B	| John |
|   prom-1jqwv15	| Gaming 	| Game B	| Jane |
|   prom-1jqwv16	| Gaming 	| Game B	| Jane |
|   prom-1jqwv17	| Gaming 	| Game B	| Jane |
|   prom-1jqwv18	| Entertainment	| Post-production	| Harry |
|   prom-1jqwv19	| Entertainment	| Post-production	| Harry |
|   prom-1jqwv110	| Entertainment	| Post-production	| Harry |

### Using Tag

- Filter out the TMP instances in the charge of Harry
    Filter out the TMP instances where the OPS owner is "Harry". For detailed directions, please see Using Tag.
- Filter out the TMP instances in the charge of Jane in the gaming department
    Filter out the TMP instances where the department is "gaming" and OPS owner is "Jane". For detailed directions, please see Using Tag.
