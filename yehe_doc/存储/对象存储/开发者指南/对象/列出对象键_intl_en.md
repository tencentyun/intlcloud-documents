An [object key](https://intl.cloud.tencent.com/document/product/436/13324) is the unique identifier of an object in a bucket. You can think of it as the object’s path. For example, if an object key is `doc/picture.jpg`, the image `picture.jpg` is stored in the `doc` path/folder in COS.

You can use the object key to search for a specific object. You can also use a prefix of the object key (e.g. `doc`) to search for all objects with this prefix (e.g. all objects prefixed with `doc`).

## Overview

Tencent Cloud COS supports listing keys by a prefix. You can use `/` in a key to implement a hierarchical structure similar to the traditional file system. In COS, you can use a delimiter to select and browse keys hierarchically.

You can list all keys in a single bucket in UTF-8 binary order of prefixes or filter the key list by specifying the prefix. For example, adding the parameter `t` will list the `tencent` object, but skip objects prefixed with `a` or other characters.

`/` can be used as a delimiter in object keys. In this way, both the prefix and delimiter can be used to facilitate the search.

COS allows you to store an unlimited number of objects in a single bucket. As a result, the key list may be very large. For the convenience of management, a maximum of 1,000 key values can be returned in each `List Objects` request, and a marker will be returned to indicate whether the list is truncated. If so, not all objects are listed in this request. In this case, you can initiate the `List Objects` request multiple times based on markers and delimiter to list all/some object keys as needed.

## Directions

### Using COS console

Search for objects in the COS console. For more information, see [Searching for Objects](https://intl.cloud.tencent.com/document/product/436/13325) in Console Guide.

### Using REST APIs

Use REST APIs to initiate a request to list object keys. For more information, see [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614).

### Using SDKs

Directly call the object list querying method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/37676)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/37685)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/32457)
