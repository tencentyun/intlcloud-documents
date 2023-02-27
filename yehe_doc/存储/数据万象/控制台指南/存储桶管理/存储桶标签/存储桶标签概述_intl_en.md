## Overview

A bucket tag is a key-value pair (key = value), where the tag key and tag value are connected by an equal sign (=), for example: group = IT. It can be used to manage buckets in groups. You can set, query, and delete the tag for a specified bucket.

## Specifications and Restrictions

### Tag key restrictions

- A tag key starting with "qcs:" or "project" is a default tag key and cannot be created.
- A tag value can only contain characters encoded in UTF-8, spaces, numbers, or special characters including `+ - = . _ : / @`.
- A tag key should be a combination of 0-127 characters encoded in UTF-8.
- Tag keys are case sensitive.

#### Tag value restrictions

- A tag value can only contain characters encoded in UTF-8, spaces, numbers, or special characters including `+ - = . _ : / @`.
- A tag value should be a combination of 0-255 characters encoded in UTF-8.
- Tag values are case sensitive.

#### Tag quantity restrictions

- Bucket dimension: A resource has at most 50 different bucket tags.
- Tag dimension:
  - A user has at most 1,000 different keys. 
  - A key has at most 1,000 values.
  - Multiple same keys are not allowed in the same bucket.

## How to Use

You can set bucket tags in the console as instructed in [Setting Bucket Tag](https://www.tencentcloud.com/document/product/1045/53781).

- If you have set a bucket tag in the COS console, the tag will be automatically obtained when you bind the bucket in the CI console.
- If you adjust or delete the bucket tag in the COS console after binding a bucket in the CI console, the bucket tag displayed in the CI console won't change.



