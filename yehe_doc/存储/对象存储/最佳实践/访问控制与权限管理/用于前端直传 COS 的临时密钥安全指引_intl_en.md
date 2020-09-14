## Overview

In mobile and Web applications, you can directly initiate requests to COS from your frontend through the SDK for iOS, Android, or JavaScript. In this way, data uploads and downloads do not pass through your backend server, which reduces its bandwidth usage and load and makes full use of various COS capabilities, such as bandwidth and global acceleration, to improve the user experience of your application.

In practice, you need to use a temporary key as the signature for a frontend COS request to avoid problems such as leakage of your permanent key and unauthorized access. However, even with a temporary signature, if you specify excessive permissions or paths, such problems may still occur, which brings certain risks to your application. This document describes some bad examples and security regulations that you need to comply with for your application to securely use COS.

## Prerequisites

This document assumes that you have a good understanding of the concepts related to temporary key, and can generate and use one to send requests to COS. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

## Bad Examples and Security Regulations

### Bad example 1. Excessive resource

Application A uses COS when registered users upload profile photos. Each user has a fixed object key `app/avatar/<Username>.jpg` for their profile photo, and another two object keys `app/avatar/<Username>_m.jpg` and `app/avatar/<Username>_s.jpg` for different photo sizes. When you generate a temporary key on the backend, you specify the `resource` as `qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/*` for convenience. In this case, when a malicious user gets the generated temporary key through methods such as packet capture, they may gain unauthorized access by uploading an image to overwrite any user's profile photo.

#### Security regulation

`resource` indicates the resource path that a temporary key can access, and end users covered by this path need to be taken into full account. In principle, the specified `resource` should be used only by a single user. In this example, the specified `qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/*` will apparently cover all users, resulting in security vulnerabilities.

In this example, the path to user's profile photo can be modified to `app/avatar/<Username>/<size>.jpg`, and `resource` can be specified as `qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>/*` to meet the security regulations. In addition, multiple values can be passed in to the `resource` field as an array. Therefore, you can explicitly specify multiple `resource` values to fully limit the final resource paths that users can access; for example:

```json
"resource": [
	"qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>.jpg",
	"qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>_m.jpg",
	"qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>_s.jpg"
]
```

### Bad example 2. Excessive action

Application B provides a public photo wall feature, and stores all photos in `app/photos/*` on COS. To use this feature, the client needs to GET Bucket and GET Object. When you generate a temporary key on the backend, you specify `action` as `name/cos:*` for convenience. In this case, a malicious user may get the generated temporary key through methods such as packet capture to gain unauthorized access to all object operations (such as upload and deletion) on any object under the resource path, which causes data loss and affects your online business.

#### Security regulation

`action` indicates operations allowed for the temporary key. A temporary key with `name/cos:*` that allows all operations should not be distributed to the frontend; instead, each required action must be explicitly listed. Besides, you need to match an “action” with a “resource” rather than concatenate multiple “actions” for the same “resource”.

In this example, you should specify `"action": [ "name/cos:GetBucket", "name/cos:GetObject" ]`. For directions on granting operation permission, see [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580).

### Bad example 3. Excessive action and resource

Application C provides a management tool that allows a user to list and download all users' files (app/files/*), but only upload and delete files in their personal directory (app/files/<Username>/*). All of these four actions are encapsulated in one backend API for convenience, and share the same resource path in the access policy. In this case, the temporary key will grant the greater permissions than otherwise specified by separate resource paths, which means the user can list, download, upload, and delete all users' files. Through this vulnerability, a malicious user can tamper with or delete other users' files and thus gain unauthorized access, which exposes valid user data to risks.

#### Security regulation

For multiple `action` and `resource` values, you should not simply concatenate them. Instead, use multiple statements to match an action with a resource to avoid granting excessive permissions.

In this example, you should use the following code:

```json
"statement": [
	{
		"effect": "allow",
		"action": [
			"name/cos:GetBucket", 
			"name/cos:GetObject"
		], 
		"resource": "qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/files/*"
	},
	{
		"effect": "allow", 
		"action": [
			"name/cos:PutObject",
			"name/cos:DeleteObject"
		],
		"resource": "qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/files/<Username>/*"
	}
]
```

### Bad example 4. Unauthorized access to temporary key

Application D provides a forum service whose attachments to posts are stored in COS. This forum has different user levels. Only active users with a certain number of posts can view posts and attachments in certain sections, while some public sections are open to all.
The backend API generates temporary keys for downloading attachments in a certain section based on the section ID received from your frontend. However, in fact, the backend API cannot determine whether a requester has access to the specified section ID due to lack of proper logic. As a result, anyone can request this API for a temporary key and gain unauthorized access to attachments in a private section, leading to potential data leakage.

#### Security regulation

For your API that generates temporary keys, you should make sure that the temporary keys grant permissions as expected, and only to the correct requesters as needed in order to avoid unauthorized access by users with lower permission.

In this example, your API should also be able to determine whether the requester has access to a specific forum section, and deny the request if it determines not.

## Summary

The examples above illustrate the security risks that may occur if permissions of a temporary key are more excessive than expected. In these cases, malicious users can get a temporary key more easily than when accessing COS through the backend, so you need to tighten your permission control.

The security regulations mentioned in this document are based on the minimum permission principle. In practice, you can enumerate all possible scenarios based on the `action` and `resource`. For example, 3 action values and 2 resource values can result in 3 * 2 = 6 application scenarios. You can evaluate whether the permissions are granted as expected based on this enumeration; and if not, you should consider using multiple statements to specify permissions.

You are also supposed to take authentication seriously for the temporary key generation API. Every precaution must be taken to protect your temporary keys.
