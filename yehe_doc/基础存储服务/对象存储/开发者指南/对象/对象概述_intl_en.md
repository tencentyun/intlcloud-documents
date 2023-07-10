## Overview

Object is the basic unit of storage in COS, which can be understood as data in any format, such as images, documents, and audio/video files. Bucket is the carrier of objects. One bucket can contain any number of objects. Different storage classes can be specified for objects in COS. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

Each object consists of an object key (ObjectKey), an object value (Value), and object metadata (Metadata).

- ObjectKey: The unique identifier of an object in a bucket, which can be regarded as the file path. In the API and SDK samples, objects are named in the format of `<ObjectKey>`.
- Value: The uploaded object itself, which can be commonly understood as the object content.
- Metadata: A set of key-value pairs, which can be regarded as file attributes, such as file modification time and storage class. You can query them after uploading the object.


## Object Key

An object in COS must contain a valid `ObjectKey` as the unique identifier of the object in a bucket.
For example, in an object's access address `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/folder/picture.jpg`, the object key is `folder/picture.jpg`.

### Naming conventions

- You can use any UTF-8 characters in an object key name. However, we recommend you use letters and digits to ensure optimal compatibility with other applications..
- The encoded length can be up to 850 bytes.
- The name cannot start with a forward slash `/` or backslash <code>\\</code>.
- An object key cannot contain certain ASCII control characters, including upward arrow (↑), downward arrow (↓), rightward arrow (→), and leftward arrow (←), corresponding to CAN (24), EM (25), SUB (26), and ESC (27) respectively.
- Refrain from using special symbols such as `*` and `%` in the filename.

>? If the name of the uploaded file or folder contains Chinese characters, when you access or request the file or folder, the Chinese characters will be converted into a percent-encoded string based on URL-encoding rules.
> For example, when you access `XXX.doc`, the object key is `XXX.doc`, but the percent-encoded string actually read is `%e6%96%87%e6%a1%a3.doc`.
> 


The following are examples of valid object key names:
- doc/exampleobject
- my.great_photos-2016/01/me.jpg
- videos/2016/birthday/video.wmv

#### Special symbols

Certain characters may need to be URL-encoded or referenced in the hexadecimal format. Some of them are non-printable characters, and your browser may not be able to handle them. They require special handling as detailed below:

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
      <td>ASCII character ranges: 00–1F hexadecimal (0–31 decimal) and 7F (127 decimal)</td>
      <td>(space)</td>
      <td></td>
   </tr>
</table>


There are also some characters that require significant special handling to maintain consistency across all applications, so we recommend you avoid them directly as detailed below:
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
      <td>*</td>
      <td>></td>
      <td><</td>
      <td>ASCII <br>128–255 decimal</td>
   </tr>
</table>

### Object access address

The access address of an object consists of a bucket access address and an object key in the format of `<bucket domain name>/<object key>`.
For example, after you upload the `exampleobject.txt` object to the `examplebucket-1250000000` bucket in Guangzhou (South China) region, the access address for `exampleobject.txt` is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`.

### Folder and directory

As COS comes with no folders or directories, it will not create a `project` folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COSBrowser. This is implemented by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example, when you upload the object `project/doc/a.txt` via APIs or SDKs, the separator `/` simulates the display mode of "folder", and you can see the folders `project` and `doc` in the console. The folder `doc` is displayed under the folder `project` and contains the file `a.txt`.

>! Objects in the bucket are evenly distributed among distributed clusters. Therefore, you cannot directly get the size of all objects with a specified object key prefix. Instead, you can accumulate the size of each object to get the full size.
>

Deleting folders and directories is relatively complicated as detailed below:

| Deletion Method | Object or Folder Deletion  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                            | Result                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| Console | Folder `project` | All objects with the object key prefix `project/` will be deleted. |
| Console | Object `project/doc/a.txt` | The `project` and `doc` folders will be retained. |
| API and SDK | Object `project/` or `project/doc/` | The object `project/doc/a.txt` will be retained. If you want to delete the objects in the folder, use code traversal to delete them. |


## Object metadata

Object metadata (or HTTP header) is a set of key-value pairs in an object. It is the string sent by the server before the server sends HTML data over the HTTP protocol to the browser. Modifying the HTTP header when uploading an object can alter page response forms or communicate configuration information, such as modifying caching time. 

There are two types of metadata: system metadata and user-defined metadata.

>? Modifying an object's HTTP header does not modify the object itself.
>

### System metadata

This refers to the attribute information of an object, such as object modification time, object size, and storage class.

<table>
<thead>
<tr>
<th width="25%">Name</th>
<th width="75%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Content-Length</td>
<td>The length of the content of an HTTP request in bytes as defined in RFC 2616</td>
</tr>
<tr>
<td>Last-Modified</td>
<td>The creation date or last modified date of an object (whichever is later)</td>
</tr>
<tr>
<td>x-cos-version-id</td>
<td>Object version ID. If versioning is enabled for a bucket, the version ID of the object will be returned to identify the historical versions of the object.</td>
</tr>
<tr>
<td>ETag</td>
<td>The MD5 value of an object uploaded by calling `PUT Object`, or the unique ID of an object uploaded by multipart upload or a legacy API (which cannot perform check though).</td>
</tr>
</tbody></table>



### User-defined metadata

This refers to the object's custom parameters, such as Content-Type, Cache-Control, Expires, and x-cos-meta-\*. For more information, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

<table>
<thead>
<tr>
<th width="25%">Name</th>
<th width="76%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Cache-Control</td>
<td>The caching policy as defined in RFC 2616, which is saved as part of the object metadata.</td>
</tr>
<tr>
<td>Content-Disposition, <br>Content-Encoding, <br>Content-Type</td>
<td>The filename/encoding format/content type (MIME) as defined in RFC 2616, which are saved as part of the object metadata.</td>
</tr>
<tr>
<td>Expires</td>
<td>The cache expiration time as defined in RFC 2616, which is saved as part of the object metadata.</td>
</tr>
<tr>
<td>x-cos-acl</td>
<td>ACL attributes of an object. Valid values: `private`, `public-read-write`, `public-read`. Default value: `private`.</td>
</tr>
<tr>
<td>x-cos-grant-*</td>
<td>Grants the grantee permissions.</td>
</tr>
<tr>
<td>x-cos-meta-*</td>
<td>User-defined header, which is returned as part of the object metadata with a size up to 2 KB.</td>
</tr>
<tr>
<td>x-cos-storage-class</td>
<td>Storage class of an object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD`.</td>
</tr>
<tr>
<td>x-cos-server-side-encryption</td>
<td>Specifies whether to enable server-side encryption for the object and the encryption method.</td>
</tr>
</tbody></table>


## Object Operations

You can manage objects through the Tencent Cloud console, tools, APIs, and SDKs.

>!Objects can be uploaded via [simple upload](https://intl.cloud.tencent.com/document/product/436/14113) or [multipart upload](https://intl.cloud.tencent.com/document/product/436/14112) based on the object size.
>- Use simple upload for objects less than 5 GB in size.
>- Multipart upload is limited to no more than 10,000 parts (each in 5 GB) and a maximum object size of around 48.82 TB. For more information on use limits, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

After uploading objects, you can configure them in the console. For more information, see:

- [Searching for Objects](https://intl.cloud.tencent.com/document/product/436/13325)
- [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326)
- [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327)
- [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361)

## Object Subresource

COS has subresources that are associated with buckets and objects. Subresources are subordinates to objects, so they do not exist on their own. They are always associated with other entities such as objects or buckets. An ACL is the access control information list for a specific COS object, which is a subresource of the object.

An ACL contains an authorization list that identifies authorized users and the granted permissions to implement access control on the object. When an object is created, the ACL identifies the object owner who can fully control the object. You can search for the object ACL or replace it with a new one.

>? You can update an ACL only by replacing it.
>

## Access Permission Types

COS supports setting two permissions for objects: **public permissions** and **user permissions**.
**Public permissions**: Include **Inherit**, **Private Read/Write**, and **Public Read/Private Write**.
- Inherit: The object inherits the access permission of the bucket. When you access an object with the inherited bucket permission, COS will match the bucket permission to respond to the access request. A new object inherits the permission from its bucket by default.
- Private Read/Write: When you access an object with the private read/write permission, the object can only be accessed with a [request signature](https://intl.cloud.tencent.com/document/product/436/7778), regardless of the bucket access permission.
- Public Read/Private Write: When you access an object with the public read permission, the object can be directly downloaded, regardless of the bucket access permission.

**User permissions**: A root account has all the permissions (full access) of buckets by default. In addition, you can add sub-accounts and grant them permissions to read/write data and permissions and even get full access.

#### Use cases
Allow public access to a specified object in a private read/write bucket, or require authentication for a specific object in a public read/write bucket.
