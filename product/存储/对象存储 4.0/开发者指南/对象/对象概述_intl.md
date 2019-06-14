## Definition

An object is the basic unit of COS, and is stored in a bucket just like a photo stored in an album. You can manage objects in different ways including Tencent Cloud Console, APIs, and SDKs. Its naming format is `<ObjectKey>`.

>Objects can be uploaded via simple upload or multipart upload.
>- Use simple upload for objects less than 5 GB.
>- Multipart upload is limited to not more than 10,000 parts of 5 GB each and a maximum object size of 48.82 TB.

Each object consists of the ObjectKey, Value, and Metadata.

- ObjectKey: The unique identifier of the object in the bucket.
- Value: The size of the uploaded object.
- Metadata: A set of name-value pairs that you can set when you upload an object.

You can configure related objects on the console. For more information, see:

- [Searching for Objects](https://intl.cloud.tencent.com/document/product/436/13325)
- [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326)
- [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327)
- [Setting Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361)

## ObjectKey

### Definition

An object in Tencent Cloud COS must contain a valid ObjectKey. An ObjectKey is the unique identifier of an object in a bucket.
For example, in the object's access address `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/folder/picture.jpg`, its ObjectKey is `folder/picture.jpg`.

### Naming conventions

- You can use any UTF-8 character in a key name. However, for the maximum compatibility with other applications, it is recommended to use uppercase and lowercase letters and numbers, i.e. [a-z, A-Z, and 0-9], special characters (`-`, `!`, `_`, `.`, and `*`), and the combination of them.
- The maximum encoding length is 850 bytes.
- A key does not support some ASCII control characters, including upward arrow (↑), downward arrow (↓), rightward arrow (→), and leftward arrow (←), corresponding to CAN (24), EM (25), SUB (26), and ESC (27).
- If the name of the uploaded file or folder contains Chinese characters, when you access or request the file or folder, the Chinese characters are converted into a percent-encoded string according to URL Encode rules.
For example, when you access `文档.doc`, the object key is `文档.doc`, but the percent-encoded string you read is `%e6%96%87%e6%a1%a3.doc`.

The following are examples of valid key names:

- my-organization
- my.great_photos-2016/01/me.jpg
- videos/2016/birthday/video.wmv

#### Special characters

Some characters may need to be URL encoded or referenced in the hexadecimal format. Some of these are non-printable characters and your browser might not handle them, which also requires special handling, as shown below:

|  ，  |                              :                               |    ;     |  =   |
| :--: | :----------------------------------------------------------: | :------: | :--: |
|  &   |                              $                               |    @     |  +   |
| ? | ASCII character ranges: 00-1F hexadecimal (0-31 decimal) <br />and 7F (127 decimal) | (Space) |      |

There are also some characters that require significant special handling to maintain consistency across all applications, so it is recommended to avoid them directly, as shown below:

|  `   |  ^   |             "              |  \|
| :--: | :--: | :------------------------: | :--: |
|  {   |  }   |             [              |  ]   |
|  ~   |  %   |             #              |  \|  |
|  >   |  <   | ASCII <br />128-255 decimal ||

### Description

#### Access address

The access address of the object consists of a bucket access address and an object key, in the format of `[bucket domain name]/[object key]`.

For example, when you upload the `exampleobject.txt` object to the `examplebucket-1250000000` bucket in Guangzhou (South China), the access address for `exampleobject.txt` is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`.

#### Folder and directory

As COS comes with no folders and directories, it will not create a `project` folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example: When you upload the object `project/doc/a.txt` via APIs or SDKs, the delimiter `/` simulates the display mode of "folder", and you can see the folders `project` and `doc` in the console. The folder `doc` is displayed under the folder `project` and contains the file `a.txt`.

>Objects in the bucket are evenly distributed among distributed clusters. Therefore, you cannot directly get the size of all objects with a specified key prefix. Instead, you can accumulate the size of each object to get the full size.

Deleting folders and directories is relatively complicated, as shown below:

| Method | Delete                              | Result                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| Console | Folder `project` | All objects with the key prefix `project/` will be deleted. |
| Console | Object `project/doc/a.txt` | The `project` and `doc` folders will be retained. |
| API and SDK | Object `project/` or `project/doc/` | The object `project/doc/*.txt` will be retained. If you want to delete the objects in the folder, use code traversal to delete the objects in the folder. |

## Storage Classes

COS provides three object storage classes based on the access frequency: COS Standard, COS Infrequent Access, and Archive Storage.

>The default storage class is COS Standard.

### COS Standard

COS Standard provides users with high-reliability, high-availability and high-performance storage.

COS Standard features low access latency and high throughput,  making it well suited for use cases where a large number of hot files and frequent data access are needed.

**Use Cases**: Hotspot videos, social images, mobile Apps, game programs, and dynamic websites.

### COS Infrequent Access

COS Infrequent Access is a high-reliability, high-availability, low-cost, and low-latency storage service.

You can cut your storage cost while still accessing the first byte in milliseconds. When retrieving data, you are able to quickly read data without waiting. Data retrieval is paid so COS Infrequent Access is suited for uses cases with infrequent access.

**Use Cases**: Network disk data, big data analysis, government and enterprise business data, infrequent access archives, and monitoring data.

### Archive Storage

Archive Storage features high-availability, extra-low storage cost and long-term data retention.

Archive Storage has the lowest storage price but a relatively long data reading time, and is well suited for storing archived data which needs to be kept for a long time.

**Use Cases**: Archive data, medical images, scientific data, and film and video materials.

### Comparison

| | COS Standard | COS Infrequent Access | Archive Storage |
| ------------ | -------- | -------- | ------------------- |
| Response | Millisecond | Millisecond | Request for recovery in advance |
| Minimum billing period | - | 30 days | 90 days |
| Supported regions | All regions | All regions | Only Mainland China |
| Storage fee | Standard | Low | Extra-low |
| Data retrieval fee | - | Low | High |
| Read/Write request fee | Extra-low | Low | Extra-low (read/write only after recovery) |


## Metadata

### Definition

Metadata or HTTP Header, is a set of name-value pair in an object. It is the string sent by the server using HTTP protocol and afterwards the server sends HTML data to browser. Modifying the HTTP header when uploading an object can alter page response forms or communicate configuration information, such as modifying caching time. 

There are two kinds of metadata: system metadata and user-defined metadata.

>Modifying an object's HTTP header does not modify the object itself.

### System metadata

Refers to the attribute information of the object, such as upload time or modification time.

| Name | Description |
| ---------------- | ------------------------------------------------------------ |
| Date | Current date and time |
| Content-Length | HTTP request content length defined in RFC 2616 (in bytes), commonly used in API operations of PUT type. |
| Last-Modified | Object creation date or the last modified date, whichever occurs later. |
| ContentMD5 | The base64-encoded 128-bit MD5 check value defined in RFC 1864. This header is used to verify whether the file content has changed. |
| Authorization | Authentication information, such as signature information used to verify the validity of requests. For public read files, this header is not required. |
| x-cos-version-id | Object version. When you enable version control on a bucket, the version ID of the object is returned. |
| ETag | Indicates the MD5 value of the uploaded file if the object is uploaded by PUT Object; indicates the unique ID of the uploaded file if the object is uploaded by multipart upload or using the earlier versions of APIs, but it cannot perform check. |
| Expect | HTTP request length defined in RFC 2616 (in bytes) |
| Connection | Connection status between the client and server. Enumerated values: keep-alive and close |

### User-defined metadata

Refers to the object's custom parameters, such as Content-Type, Cache-Control, Expires, and x-cos-meta-. For more information, see [Custom Object Headers](https://cloud.tencent.com/document/product/436/13361).

| Name | Description |
| --------------------------------- | ------------------------------------------------------------ |
| Cache-Control | The caching policy defined in RFC 2616, which will be saved as Object metadata. |
| Content-Disposition/Encoding/Type | The file name/encoding format/content type (MIME) defined in RFC 2616, which will be saved as Object metadata. |
| Expires | The file name defined in RFC 2616, which will be saved as Object cache expiration time. |
| x-cos-acl | Defines the ACL attribute of an Object. Valid values: private, public-read-write, and public-read. Default: private |
| x-cos-grant-* | Grants permission to the authorized user. |
| x-cos-meta- * | The header information allowed to be defined by users, which is returned as Object metadata. The size is limited to 2 KB. |
| x-cos-storage-class | Sets the storage class of an Object. Enumerated values: STANDARD and STANDARD_IA. Default: STANDARD |
| x-cos-server-side-encryption | Indicates whether server-side encryption is enabled for the object. If you use COS master key for encryption, enter AES256. |

## Object Sub-resources

COS has sub-resources that are associated with buckets and objects. Sub-resources belong to objects, so sub-resources do not exist independently but are always associated with other entities such objects or buckets. An Access Control List (ACL) is the access control information list for a specific object, which is a sub-resource of a COS object.

An ACL contains an authorization list that identifies authorized users and the granted licenses to implement access control on the object. When you create an object, ACL identifies the object owner who can fully control the object. The user can retrieve the object ACL or replace it with a new authorization list.

>For any updates to the ACL, replace the existing ACL.

## Access Permission Types

COS supports setting two permissions for objects: **Public Permissions** and **User Permissions**.
**Public Permissions**: Includes Inherit Permission, Private Read/Write, and Public Read/Private Write.
- Inherit Permission: Bucket permission inherited by an object is consistent with bucket access permission. When you access an object with the permission of "Inherit Bucket Permission", COS matches the bucket permission to respond to the access. A new object inherits the permission from its bucket by default.
- Private Read/Write: When you access an object with the permission of "Private Read/Write", the object can only be accessed after [signature authentication](/document/product/436/6054), regardless of the bucket permission.
- Public Read/Private Write: When you access an object with the permission of "Public Read", the object can be directly downloaded, regardless of the bucket permission.

**User Permissions**: The primary account has all the permissions of the object by default (i.e. full control). In COS, sub-accounts can be added to read/write data, read/write permissions, and have the full control permission.

### Use cases
You can set the specified object which allow public access in a private read/write bucket, or the specified objects which only allow access after authentication in a public read/write bucket.

