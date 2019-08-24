## Overview

A bucket tag is a key-value pair (key = value), which is comprised of a tag key and a tag value that are connected by an equal sign ("="), for example: group = IT. It can be used to identify a bucket, helping you achieve group management of buckets. You can set, query, and delete the tag for a specified bucket.

## Specifications and Limits

>! Chinese bucket tags are not supported. We will enable the feature as soon as possible. If you have any questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### Limits on Tag Keys

- A tag key starting with "qcs:" or "project" is a default tag key and cannot be changed.
- A tag key can only contain characters encoded in UTF-8, spaces, numbers, or special characters including `+, -, =, ., _, :, /, @`.
- A tag key should be a combination of 0-127 characters encoded in UTF-8.
- Tag keys are case sensitive.

### Limits on Tag Values

- A tag value can only contain characters encoded in UTF-8, spaces, numbers, or special characters including `+, -, =, ., _, :, /, @`.
- A tag value should be a combination of 0-255 characters encoded in UTF-8.
- Tag values are case sensitive.

### Limits on the Number of Tags

- Bucket dimension: A resource has at most 10 different bucket tags.
- Tag dimension:
 - A user has at most 1,000 different keys. 
 - A key has at most 1,000 values.
 - Multiple same keys are not allowed in the same bucket.

## Usage

You can set bucket tags via the console or APIs.

### Via the COS Console

For more information on how to set a bucket tag using the COS Console, see [Setting Bucket Tags](https://cloud.tencent.com/document/product/436/34830) in Console Guide.

### Via REST APIs

You can directly manage bucket tags using the following APIs:

- [PUT Bucket tagging](https://cloud.tencent.com/document/product/436/34838)
- [GET Bucket tagging](https://cloud.tencent.com/document/product/436/34837)
- [DELETE Bucket tagging](https://cloud.tencent.com/document/product/436/34836)

