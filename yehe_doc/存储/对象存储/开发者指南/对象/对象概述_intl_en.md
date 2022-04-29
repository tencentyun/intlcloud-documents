## Overview

Object is the basic unit of storage in COS, which can be understood as data in any format, such as images, documents, and audio/video files. Bucket is the carrier of objects. One bucket can contain any number of objects. Different storage classes can be specified for objects in COS. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

Each object consists of an object key (ObjectKey), an object value (Value), and object metadata (Metadata).

- ObjectKey: The unique identifier of the object in the bucket, which can be regarded as the file path. In the API and SDK samples, objects are named in the format of `<ObjectKey>`.
- Value: The uploaded object, which can be regarded as the object content.
- Metadata: A set of key-value pairs, which can be regarded as object attributes, such as modification time and storage class. You can query it after uploading an object.



## Object Key

An object in COS must contain a valid object key (ObjectKey), which is its unique identifier in a bucket.
For example, in an object's access address `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/folder/picture.jpg`, the object key is `folder/picture.jpg`.

### Naming conventions

- You can use any UTF-8 characters in an object key name. However, for the maximum compatibility with other applications, we recommend you use letters (a-z, A-Z), digits (0-9), and special characters (`-`, `!`, `_`, `.`, and `*`).
- The encoding length can be up to 850 bytes.
- It cannot start with a forward slash (/) or a backslash (\).
- An object key cannot contain certain ASCII control characters, including upward arrow (↑), downward arrow (↓), rightward arrow (→), and leftward arrow (←), corresponding to CAN (24), EM (25), SUB (26), and ESC (27) respectively.


The following are examples of valid object key names:
- doc/exampleobject
- my.great_photos-2016/01/me.jpg
- videos/2016/birthday/video.wmv

#### Special characters

Certain characters may need to be URL- encoded or referenced in the hexadecimal format. Some of them are non-printable characters and your browser might not be able to handle them. They'd require special handling, as shown below:

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
      <td>?</td>
      <td>ASCII character range: 00-1F hexadecimal (0-31 decimal) and 7F (127 decimal)</td>
      <td>(space)</td>
      <td></td>
   </tr>
</table>



There are also some characters that require heavy special handling to maintain consistency across all applications, so we recommend you avoid them directly, as shown below:
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

### Object access address

The access address of an object consists of a bucket access address and an object key in the format of `<bucket domain name>/<object key>`.
For example, when you upload the `exampleobject.txt` object to the `examplebucket-1250000000` bucket in Guangzhou (South China), the access address for `exampleobject.txt` is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`.

### Folder and directory

As COS comes with no folders or directories, it will not create a `project` folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COSBrowser. This is implemented by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example, when you upload the object `project/doc/a.txt` through APIs or SDKs, the delimiter `/` simulates the display mode of "folder", and you can see the folders `project` and `doc` in the console. The folder `doc` is displayed under the folder `project` and contains the file `a.txt`.

>!Objects in the bucket are evenly distributed among distributed clusters. Therefore, you cannot directly get the size of all objects with a specified object key prefix. Instead, you can accumulate the size of each object to get the full size.

Deleting folders and directories is relatively complicated, as shown below:

| Deletion Means | Object or Folder Deletion                            | Result                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| Console | Folder `project` | All objects with the object key prefix `project/` will be deleted |
| Console | Object `project/doc/a.txt` | The `project` and `doc` folders will be retained |
| API and SDK | Object `project/` or `project/doc/` | The object `project/doc/a.txt` will be retained. If you want to delete the objects in the folder, use code traversal to delete them |


## Object Metadata

Metadata (or HTTP header) is a set of key-value pairs in an object. It is the string sent by the server before the server sends HTML data over HTTP protocol to the browser. Modifying the HTTP header when uploading an object can alter page response forms or communicate configuration information, such as modifying caching time. 

There are two types of metadata: system metadata and user-defined metadata.

>?Modifying an object's HTTP header does not modify the object itself.

### System metadata

This refers to the attribute information of the object, such as object modification time, object size, and storage class.

<table>
<thead>
<tr>
<th width="25%">Name</th>
<th width="75%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Content-Length</td>
<td>Length in bytes of the content of an HTTP request defined in RFC 2616</td>
</tr>
<tr>
<td>Last-Modified</td>
<td>The creation date or last modified date (whichever is later) of the object</td>
</tr>
<tr>
<td>x-cos-version-id</td>
<td>Object version ID. If versioning is enabled for a bucket, the version ID of the object will be returned to identify the historical versions of the object</td>
</tr>
<tr>
<td>ETag</td>
<td>Indicates the MD5 value of an object uploaded by calling PUT Object, or the unique ID of an object uploaded by multipart upload or a historical version of API, which cannot perform check though</td>
</tr>
</tbody></table>



### User-defined metadata

This refers to the object's custom parameters, such as Content-Type, Cache-Control, Expires, and x-cos-meta-\*. For more information, see [Custom Object Headers](https://intl.cloud.tencent.com/document/product/436/13361).

<table>
<thead>
<tr>
<th width="25%">Name</th>
<th width="76%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Cache-Control</td>
<td>The caching policy as defined in RFC 2616; saved as part of object metadata</td>
</tr>
<tr>
<td>Content-Disposition, <br>Content-Encoding, <br>Content-Type</td>
<td>File name/encoding format/content type (MIME) as defined in RFC 2616; saved as part of object metadata</td>
</tr>
<tr>
<td>Expires</td>
<td>The cache expiration time as defined in RFC 2616; saved as part of object metadata</td>
</tr>
<tr>
<td>x-cos-acl</td>
<td>Defines ACL attributes of the object. Valid values: private, public-read-write, public-read. Default value: private</td>
</tr>
<tr>
<td>x-cos-grant-*</td>
<td>Grants the grantee permissions</td>
</tr>
<tr>
<td>x-cos-meta-*</td>
<td>User-defined headers; returned as part of object metadata with a size up to 2 KB </td>
</tr>
<tr>
<td>x-cos-storage-class</td>
<td>Storage class of the object; enumerated values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD</td>
</tr>
<tr>
<td>x-cos-server-side-encryption</td>
<td>Specifies whether to enable server-side encryption for the object and the encryption method</td>
</tr>
</tbody></table>


## Object Operations

You can manage objects through the Tencent Cloud console, tools, APIs, and SDKs.

>!According to the maximum file size supported for upload, there are two upload methods: [simple upload](https://intl.cloud.tencent.com/document/product/436/14113) and [multipart upload](https://intl.cloud.tencent.com/document/product/436/14112).
>- Use simple upload for objects less than 5 GB.
>- Multipart upload is limited to no more than 10,000 parts (each in 5 GB) and a maximum object size of around 48.82 TB. For more information on the use limits, please see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

After an object is uploaded, you can configure it in the console. For more information, please see:

- [Searching for Objects](https://intl.cloud.tencent.com/document/product/436/13325)
- [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326)
- [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327)
- [Setting Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361)

## Object Subresources

COS has subresources that are associated with buckets and objects. Subresources are subordinates to objects, so they do not exist on their own. They are always associated with other entities such as objects or buckets. An access control list (ACL) is the access control information list for a specific object, which is a subresource of a COS object.

An ACL contains an authorization list that identifies authorized users and the granted permissions to implement access control on the object. When you create an object, ACL identifies the object owner who can fully control the object. You can retrieve the object ACL or replace it with a new authorization list.

>?To update an ACL, you can only do so by replacing it.

## Access Permission Types

COS supports setting two types of permissions to objects: **public permissions** and **user permissions**.
**Public Permissions**: Includes Inherit Permission, Private Read/Write, and Public Read/Private Write.
- Inherited permission: The object permissions inherited from the bucket is the same as the access permissions of the bucket itself. When you access an object with the "inherited bucket permission", COS will match the bucket permission to respond to the access. A new object inherits the permission from its bucket by default.
- Private Read/Write: When you access an object with the Private Read/Write permission, the object can only be accessed with a [request signature](https://intl.cloud.tencent.com/document/product/436/7778), regardless of the bucket permission.
- Public Read/Private Write: When an object with an access permission of "Public Read" is accessed, the object can be directly downloaded, regardless of the bucket access permission.

**User permissions**: A root account has all the permissions (full access) for buckets by default. In addition, you can add sub-accounts that are granted permissions to read/write data and permissions, and even full access.

#### Use cases
Allow public access to a specified object in a Private Read/Write bucket or require authentication for a specific object in a Public Read/Write bucket.
