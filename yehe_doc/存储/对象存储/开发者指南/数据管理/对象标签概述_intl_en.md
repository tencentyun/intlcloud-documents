## Overview

Object Tagging is designed to help you group and manage objects in your bucket by adding a key-value pair as an object tag. An object tag consists of a `tagKey`, a `=`, and a `tagValue`, such as `group = IT`. You can set, query, and delete tags on the specified object.

>You will be billed for using this feature. For more information on its pricing, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

## Directions

### Using COS console

You can manage object tags in the COS console. For more information, see [Setting Object Tags](https://intl.cloud.tencent.com/document/product/436/35664).

### Using RESTful APIs

You can manage object tags via the following APIs:

- [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709)
- [GET Object  tagging](https://intl.cloud.tencent.com/document/product/436/35710)
- [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711)

## Specifications and Restrictions

### Tag key restrictions

- You cannot create tag keys starting with `qcs:`, `project`, or any other system reserved characters.
- A tag key can only contain UTF-8 encoded letters, spaces, numbers, and special characters `+ - = . _ : / @`.
- A tag key can be 1-127 characters encoded in UTF-8.
- Tag keys are case-sensitive.

### Tag value restrictions

- A tag value can only contain UTF-8-encoded letters, spaces, numbers, and special characters `+ - = . _ : / @`.
- A tag value can be 1-127 characters encoded in UTF-8.
- Tag values are case-sensitive.

### Restrictions on the number of tags

- Object dimension: Up to 10 different tags for one object.
- Tag dimension: Unlimited.

