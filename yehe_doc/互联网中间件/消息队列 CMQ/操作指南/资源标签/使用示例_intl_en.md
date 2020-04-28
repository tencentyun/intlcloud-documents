>The CMQ resource tagging feature was relaunched on September 9, 2019, which is automatically compatible with previously configured resource tags.

## Overview
A resource tag is a key-value pair provided by Tencent Cloud to identify a resource in the cloud.
You can use resource tags to classify CMQ resources based on various factors such as service, usage, and person in charge. With resource tags, you can quickly sift through the resource pool and find the corresponding resources. The values of resource tag keys do not mean anything to Tencent Cloud semantically and will be parsed and matched strictly according to the string.
Below is a specific use case to show how a resource tag is used.

## Use Case Background
A company owns 10 CMQ instances in Tencent Cloud. Distributed in three departments (ecommerce, gaming, and entertainment), these instances are used to serve internal business lines such as marketing, game A, game B, and post-production. The OPS owners of the three departments are John, Jane, and Harry, respectively.

## Directions
### Setting resource tag
To facilitate management, the company categorizes its CMQ resources with resource tags and defines the following resource tag key-value pairs:

| Resource Tag Key |	Tag Value |
|----------|----------|
| Department	| Ecommerce, gaming, and entertainment |
| Business |	Marketing, game A, game B, and post-production |
| OPS owner	| John, Jane, and Harry |

These resource tags are bound to CMQ instances in the following way:

| ID	|Department	|Business	|OPS Owner|
|---|-------|--------|---------|
|queue-pale1	| Ecommerce	| Marketing	| Harry |
|queue-pale12	| Ecommerce	| Marketing	| Harry |
|queue-pale13	| Gaming 	| Game A	| John |
|queue-pale13	| Gaming 	| Game B	| John |
|queue-pale14	| Gaming 	| Game B	| John |
|queue-pale15	| Gaming 	| Game B	| Jane |
|queue-pale16	| Gaming 	| Game B	| Jane |
|queue-pale17	| Gaming 	| Game B	| Jane |
|queue-pale18	| Entertainment	| Post-production	| Harry |
|queue-pale19	| Entertainment	| Post-production	| Harry |
|queue-pale110	| Entertainment	| Post-production	| Harry |

### Using resource tag
- Filter out the CMQ instances in the charge of Harry
Filter out the CMQ instances where the OPS owner is "Harry". For detailed directions, please see [Using Resource Tags](https://intl.cloud.tencent.com/document/product/406/34251).

- Filter out the CMQ instances in the charge of Jane in the gaming department
Filter out the CMQ instances where the department is "gaming" and OPS owner is "Jane". For detailed directions, please see [Using Resource Tags](https://intl.cloud.tencent.com/document/product/406/34251).
