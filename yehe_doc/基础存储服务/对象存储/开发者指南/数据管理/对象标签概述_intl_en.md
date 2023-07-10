## Overview

Object tagging is designed to help you group and manage objects in your bucket by adding a key-value pair as an object tag. An object tag consists of a `tagKey`, a `=`, and a `tagValue`, such as `group = IT`. You can set, query, and delete tags on the specified object.

>! Object tagging is a paid feature. For detailed pricing, see [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos).
>

## Directions

### Through the COS console

You can manage object tags in the COS console as instructed in [Setting Object Tag](https://intl.cloud.tencent.com/document/product/436/35664).

### Through RESTful APIs

You can manage object tags through the following APIs:

- [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709)
- [GET Object  tagging](https://intl.cloud.tencent.com/document/product/436/35710)
- [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711)

## Specifications and Restrictions

### Tag key restrictions


- A tag key can only contain UTF-8 letters, spaces, digits, or special symbols `+ - = ._ : / @`.
- A tag key can contain 1–127 UTF-8 characters.
- Tag keys are case-sensitive.

### Tag value restrictions

- A tag value can only contain UTF-8 letters, spaces, digits, or special symbols `+ - = ._ : / @`.
- A tag value can contain 1–255 UTF-8 characters.
- Tag values are case-sensitive.

### Tag quantity restrictions

- Object dimension: Up to ten unique tags per object.
- Tag dimension: Unlimited.

