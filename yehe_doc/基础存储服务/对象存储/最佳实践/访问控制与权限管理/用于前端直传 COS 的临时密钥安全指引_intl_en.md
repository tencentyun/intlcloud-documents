## Overview

In mobile and web applications, you can directly initiate requests to COS on the frontend through the SDK for iOS, Android, or JavaScript. In this way, data upload and download do not pass through your backend server, which reduces the bandwidth usage and load of your backend server and makes full use of various capabilities of COS, such as bandwidth and global acceleration, to improve the user experience of your application.

In actual usage, you need to use a temporary key as the signature for frontend COS requests to avoid problems such as leakage of the permanent key and unauthorized access. However, even with a temporary signature, if you specify excessive permissions or paths when generating it, such problems may still occur, which brings certain risks to your application. This document describes some bad examples and security regulations that you need to comply with for your application to securely use COS.

## Prerequisites

This document assumes that you have a good understanding of the concepts related to temporary key and can generate and use a temporary key to send requests to COS. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

>! When authorizing access with a temporary key, ensure that you follow the principle of the least privilege as needed. If you grant excessive permissions, such as granting permissions to all resources (`resource: *`) or all operations (`action: *`), data security risks may arise.
>

## Bad Examples and Security Regulations

### Bad example 1. Excessive `resource`

Application A uses COS when registered users upload profile photos. The profile photo of each user has a fixed object key `app/avatar/<Username>.jpg` and object keys `app/avatar/<Username>_m.jpg` and `app/avatar/<Username>_s.jpg` for different photo sizes. When you generate a temporary key on the backend, you specify `resource` as `qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/*` for convenience. In this case, when a malicious user gets the generated temporary key through methods such as packet capture, they can upload an image to overwrite any user's profile photo and thus gain unauthorized access, and the user's valid profile photo will be overwritten and lost.

#### Security regulation

`resource` indicates the resource path that a temporary key can access, and end users covered by this path need to be taken into full account. In principle, resources specified by `resource` should be used only by a single user. In this example, the specified `qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/*` will apparently cover all users, resulting in security vulnerabilities.

In this example, the path to user's profile photo can be modified to `app/avatar/<Username>/<size>.jpg`, and `resource` can be specified as `qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>/*` then to meet the security regulations. In addition, multiple values can be passed in to the `resource` field as an array. Therefore, you can explicitly specify multiple `resource` values to fully limit the final resource paths that users can access; for example:

```json
"resource": [
	"qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>.jpg",
	"qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>_m.jpg",
	"qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/app/avatar/<Username>_s.jpg"
]
```

### Bad example 2. Excessive `action`

Application B provides a public photo wall feature, where all photos are stored in `app/photos/*`, and the client needs to perform `GET Bucket` and `GET Object` operations (i.e., `action`). When you generate a temporary key on the backend, you specify `action` as `name/cos:*` for convenience. In this case, a malicious user can get the generated temporary key through methods such as packet capture to perform all object operations (such as upload and deletion) on any object under the resource path and thus gain unauthorized access, which causes data loss and affects your online business.

#### Security regulation

`action` indicates operations allowed for the temporary key. In principle, a temporary key with `name/cos:*` that allows all operations should not be distributed to the frontend; instead, all needed operations must be explicitly listed. If each operation needs different resource paths, you should match the **operation ** and **resource** path separately rather than specifying them in batches.

In this example, you should use `"action": [ "name/cos:GetBucket", "name/cos:GetObject" ]` to specify operations. For detailed directions on authorization, see [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580).

### Bad example 3. Excessive `action` and `resource`

Application C provides a management tool that allows a user to list and download all users' files (`app/files/*`) but only upload and delete files in their personal directory (`app/files/<Username>/*`). When you generate a temporary key on the backend, you mix four operations (i.e., `action`) in two permissions as well as the resource paths corresponding to the two permissions. In this case, the temporary key will have the greater permissions specified in the resource paths, that is, the user can list, download, upload, and delete all users' files. Through this vulnerability, a malicious user can tamper with or delete other users' files and thus gain unauthorized access, which exposes valid user data to risks.

#### Security regulation

For a combination of multiple `action` and `resource` values, you should not simply mix them in pair; instead, you should use multiple statements to match an `action` with the corresponding `resource` to avoid granting excessive permissions.

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

Application D provides a forum service, and attachments to posts in the forum are stored in COS. The forum application has different user levels, and only active users with a certain number of posts can view posts and attachments in certain subforums. For some public subforums, all users can view the posts and attachments.
The temporary key generation API on the COS backend will generate a temporary key that allows downloading attachments in the corresponding subforum based on the subforum ID passed in by the frontend. However, in the implementation, the backend does not check whether the requesting user has access to the subforum of the specified ID; therefore, anyone can request this API to get a temporary key that allows access to attachments in private subforums and thus gain unauthorized access. The limitation on access to private resources does not take effect, leading to potential data leakage.

#### Security regulation

In addition to making sure that the permissions of the obtained temporary key are granted as expected, the API for getting the temporary key also needs to check whether the correct permissions are requested by correct users based on the actual business scenario, so as to prevent users with low permissions from getting the temporary key for high permissions.

In this example, the backend API should also check whether the requesting user has access to the specified subforum; and if not, it should not return a temporary key.

## Summary

The examples above illustrate the security risks that may occur if permissions of a temporary key are more excessive than expected. In the scenario where files can be directly uploaded to COS on the frontend, as a malicious user can get a temporary key more easily than in the scenario where COS is accessed on the backend, you should pay more attention to permission control.

The security regulations mentioned in this document are based on the principle of least privilege. In actual usage, you can enumerate all possible permissions based on `action` and `resources`. For example, three `action` values and two `resource` values can form 3 * 2 = 6 accessible resources and corresponding operations. You can evaluate whether the permissions are granted as expected based on this enumeration; and if not, you should consider enumerating multiple statements to separate permissions.

In addition, you should take authentication into full account for the temporary key generation API. Only when the operation of getting the temporary key is secure can the obtained temporary key be truly secure. There must be no omissions on the security chain.
