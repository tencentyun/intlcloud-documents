## Definition

An object is the basic unit of COS and is stored in a bucket just like a photo stored in an album. You can manage objects in different ways including Tencent Cloud Console, APIs, and SDKs. An object is named in the format of `<ObjectKey>`.

>! Objects can be uploaded via simple upload or multipart upload.
>- Use simple upload for objects less than 5 GB.
>- Multipart upload is limited to no more than 10,000 parts (less than 5 GB per part) and a maximum object size of 48.82 TB.

Each object consists of an object key (ObjectKey), a data value (Value), and object metadata (Metadata).

- ObjectKey: the unique identifier of the object in the bucket.
- Value: the size of the uploaded object.
- Metadata: a set of name-value pairs that you can set when you upload an object.

You can configure objects in the console. For more information, see:

- [Searching for Objects](https://intl.cloud.tencent.com/document/product/436/13325)
- [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326)
- [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327)
- [Setting Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361)

## ObjectKey

#### Definition

An object in COS must contain a valid ObjectKey, which is the unique identifier of an object in a bucket.
For example, in an object's access address `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/folder/picture.jpg`, the ObjectKey is `folder/picture.jpg`.

#### Naming Convention

- You can use any UTF-8 character in a key name. However, for the maximum compatibility with other applications, it is recommended to use uppercase and lowercase letters and numbers (i.e., [a-z, A-Z, 0-9]), special characters (`-`, `!`, `_`, `.`, and `*`), and a combination of them.
- The encoding length is up to 850 bytes.
- An object key does not support some ASCII control characters, including upward arrow (↑), downward arrow (↓), rightward arrow (→), and leftward arrow (←), corresponding to CAN (24), EM (25), SUB (26), and ESC (27).
- If the name of the uploaded file or folder contains Chinese characters, when you access or request the file or folder, the Chinese characters will be converted into a percent-encoded string according to URL-encoding rules.
For example, when you access `文档.doc`, the object key is `文档.doc`, while the percent-encoded string read is `%e6%96%87%e6%a1%a3.doc`.

The following are examples of valid key names:
- `my-organization`
- `my.great_photos-2016/01/me.jpg`
- `videos/2016/birthday/video.wmv`

#### Special Characters

Certain characters may need to be URL- encoded or referenced in the hexadecimal format. Some of them are non-printable characters and your browser might not be able to handle them. They’d require special handling, as shown below:

<table>
   <tr>
	 <td>,</td>
      <td>:</td>
      <td>;</td>
      <td>=</td>
   </tr>
   <tr>
      <td>&</td>
      <td>$</td>
      <td>@</td>
      <td>+</td>
   </tr>
   <tr>
      <td></td>
      <td>ASCII character ranges: 00-1F hexadecimal (0-31 decimal) and 7F (127 decimal)</td>
      <td>(space)</td>
      <td></td>
   </tr>
</table>



There are also some characters that require significant special handling to maintain consistency across all applications, so it is recommended to avoid them directly, as shown below:
<table>
   <tr>
      <td>`</td>
      <td>^</td>
      <td>"</td>
      <td>\</td>
   </tr>
   <tr>
      <td>{</td>
      <td>}</td>
      <td>[</td>
      <td>]</td>
   </tr>
   <tr>
      <td>~</td>
      <td>%</td>
      <td>#</td>
      <td>|</td>
   </tr>
   <tr>
      <td>></td>
      <td><</td>
      <td>ASCII <br>128-255 decimal</td>
			<td></td>
   </tr>
</table>

#### Access Address

The access address of the object consists of a bucket access address and an object key, in the format of `[bucket domain name]/[object key]`.
For example, when you upload the `exampleobject.txt` object to the `examplebucket-1250000000` bucket in Guangzhou (South China), the access address for `exampleobject.txt` is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`.

#### Folder and Directory

As COS comes with no folders or directories, it will not create a `project` folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is implemented by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example, when you upload the object `project/doc/a.txt` via APIs or SDKs, the delimiter `/` simulates the display mode of "folder", and you can see the folders `project` and `doc` in the console. The folder `doc` is displayed under the folder `project` and contains the file `a.txt`.

> Objects in the bucket are evenly distributed among distributed clusters. Therefore, you cannot directly get the size of all objects with a specified object key prefix. Instead, you can accumulate the size of each object to get the full size.

Deleting folders and directories is relatively complicated, as shown below:

| Deletion Means | Deletion  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                            | Result                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| Console | Folder `project` | All objects with the object key prefix `project/` will be deleted |
| Console | Object `project/doc/a.txt` | The `project` and `doc` folders will be retained |
| API and SDK | Object `project/` or `project/doc/` | The object `project/doc/*.txt` will be retained. If you want to delete the objects in the folder, use code traversal to delete them |


## Metadata

#### Definition

Metadata (aka HTTP header) is a set of name-value pairs in an object. It is the string sent by the server before the server sends HTML data using HTTP protocol to the browser. Modifying the HTTP header when uploading an object can alter page response forms or communicate configuration information, such as modifying caching time. 

There are two types of metadata: system metadata and user-defined metadata.

> Modifying an object's HTTP header does not modify the object itself.

#### System Metadata

This refers to the attribute information of the object, such as upload time or modification time.

| Name | Description |
| ---------------- | ------------------------------------------------------------ |
| Date | Current date and time |
| Content-Length | HTTP request content length in bytes as defined in RFC 2616, commonly used in API operations of PUT type |
| Last-Modified | Object creation date or the last modified date, whichever occurs later |
| Content-MD5 | The Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed |
| Authorization | Authentication information, such as signature information used to verify the validity of request. For Public Read files, this header is not required |
| x-cos-version-id | Object version. If versioning is enabled for a bucket, the version ID of the object will be returned |
| ETag | Indicates the MD5 value of the uploaded file if the object is uploaded by PUT Object; indicates the unique ID of the uploaded file if the object is uploaded by multipart upload or using legacy of APIs, which cannot perform check though |
| Expect | HTTP request length in bytes as defined in RFC 2616 |
| Connection | Connection status between the client and server. Enumerated values: keep-alive, close |

#### User-defined Metadata

This refers to the object's custom parameters, such as Content-Type, Cache-Control, Expires, and x-cos-meta-. For more information, see [Custom Object Headers](https://intl.cloud.tencent.com/document/product/436/13361).

| Name | Description |
| --------------------------------- | ------------------------------------------------------------ |
| Cache-Control | The caching policy as defined in RFC 2616, which will be saved as the object's metadata |
| Content-Disposition/Encoding/Type | The file name/encoding format/content type (MIME) as defined in RFC 2616, which will be saved as the object's metadata |
| Expires | Object cache expiration time. For more information, see [Expires Descriptions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.21) |
| x-cos-acl | Defines the ACL attribute of an object. Value range: private, public-read-write, public-read. Default value: private |
| x-cos-grant-* | Grants permission to the authorized user. |
| x-cos-meta- * | The header information allowed to be defined by users, which is returned as the object's metadata. The size is limited to 2 KB |
| x-cos-storage-class | Sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD |
| x-cos-server-side-encryption | Indicates whether server-side encryption is enabled for the object. If you use a COS master key for encryption, enter AES256 |

## Object Sub-resources

COS has sub-resources that are associated with buckets and objects. Sub-resources belong to objects, so they do not exist independently; instead, they are always associated with other entities such as objects or buckets. An access control list (ACL) is the access control information list for a specific object, which is a sub-resource of a COS object.

An ACL contains an authorization list that identifies authorized users and the granted permissions to implement access control on the object. When you create an object, ACL identifies the object owner who can fully control the object. You can retrieve the object ACL or replace it with a new authorization list.

> To update an ACL, you can only do so by replacing it.

## Access Permission Types

COS supports setting two types of permissions to objects: **public permissions** and **user permissions**.
**Public permissions**: Including inherited permission, Private Read/Write, and Public Read/Private write.
- Inherited permission: The object permissions inherited from the bucket is the same as the access permissions of the bucket itself. When you access an object with the "inherited bucket permission", COS will match the bucket permission to respond to the access. A new object inherits the permission from its bucket by default.
- Private Read/Write: When you access an object with the Private Read/Write permission, the object can only be accessed with a [request signature](https://intl.cloud.tencent.com/document/product/436/7778), regardless of the bucket permission.
- Public Read/Private Write: When you access an object with the Public Read permission, the object can be directly downloaded, regardless of the bucket permission.

**User permissions**: The root account has all the permissions of the object by default (i.e., full control). In COS, sub-accounts can be added to Read/Write data, Read/Write permissions, and have the full control permission.

#### Use Cases
Allow public access to a specified object in a Private Read/Write bucket or set a required authentication for a specific object in a Public Read/Write bucket.
