## Differences Between Bucket Policies, User Policies, Bucket ACLs, and Object ACLs
The differences between bucket policies, user policies, bucket ACLs, and object ACLs are as follows, which are further illustrated in Table 1:
- User policies grant permissions based on users. Bucket policies, bucket ACLs, and object ACLs grant permissions based on resources.
- User policies and bucket policies are based on the access policy language and therefore provide higher permission control flexibility. They allow you to grant the permission of each specific action and the permission effect can be set to `deny` or `allow`. Bucket ACLs and object ACLs are based on ACLs ad therefore provide relatively lower permission control flexibility. They allow you to grant only basic read and write permissions.
- User policies cannot be used to grant permissions to anonymous users. Bucket policies, bucket ACLs, and object ACLs can be used to grant permissions to anonymous users.
- User policies are configured in the CAM console. Bucket policies, bucket ACLs, and object ACLs are configured in the COS console.

**Table 1. Differences between authorization methods**
<table>
<tr>
<th colspan='2'>Item</td>
<th>User policy</td>
<td>Bucket policy</td>
<th>Bucket ACL</td>
<th>Object ACL</td>
</tr>
<tr>
<td colspan='2'>Classification</td>
<td>User-based authorization</td>
<td>Resource-based authorization</td>
<td>Resource-based authorization</td>
<td>Resource-based authorization</td>
</tr>
<tr>
<td colspan='2'>Permission control flexibility</td>
<td>High flexibility</td>
<td>High flexibility</td>
<td>Low flexibility</td>
<td>Low flexibility</td>
</tr>
<tr>
<td colspan='2'>Console configuration</td>
<td>CAM console</td>
<td>COS console</td>
<td>COS console</td>
<td>COS console</td>
</tr>
<tr>
<td rowspan='7'>Access control element</td>
<td rowspan='3'>User</td>
<td rowspan='2'>All CAM identities (sub-accounts, roles, etc.) management by the current account</td>
<td>Sub-accounts, root accounts, anonymous users</td>
<td rowspan='2'>Sub-accounts, other root accounts, anonymous users</td>
<td rowspan='2'>Sub-accounts, other root accounts, anonymous users</td>
</tr>
<tr>
<td>Sub-account Tencent Cloud services, roles, etc.</td>
</tr>
<tr>
<td>Before cross-account authorization, you need to add the target account as your collaborator.</td>
<td colspan='3' class='x21'>Directly supports cross-account authorization.</td>
</tr>
<tr>
<td>Effect</td>
<td>Allow + Deny</td>
<td>Allow + Deny</td>
<td>Allow only</td>
<td>Allow only</td>
</tr>
<tr>
<td>Resource</td>
<td>All cloud resources, all COS buckets, specified buckets (prefixes, objects, etc.)</td>
<td>Specified buckets (prefixes, objects, etc.)</td>
<td>Entire bucket</td>
<td>Specified objects</td>
</tr>
<tr>
<td>Action</td>
<td>Every specific action</td>
<td>Every specific action (excluding bucket creation and bucket listing)</td>
<td>Simplified read and write permissions</td>
<td>Simplified read and write permissions</td>
</tr>
<tr>
<td>Condition</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
</table>

## How to Choose an Appropriate Authorization Method?
The differences listed in Table 1 show the advantages and disadvantages of different authorization methods. You can choose an appropriate authorization method based on your own needs.
But whichever authorization method you choose, you are advised to maintain consistency as much as possible. Otherwise, with the increase of bucket policies, user policies, and ACLs, it will become increasingly difficult to maintain permissions.

### When do I use an ACL?

>! Enabling anonymous access (Public Read) is highly risky due to hotlinking risks. In cases where Public Read is required, you can [set hotlink protection](https://intl.cloud.tencent.com/document/product/436/13319) to improve security.
>

Use ACLs if you only need to set some simple access permissions for buckets and objects or enable anonymous access. However, in most cases, you are advised to use bucket policies or user policies, which are more flexible. ACLs are recommended in scenarios where you want to:
- Set simple access permissions.
- Set access permissions quickly in the console.
- Make an object, directory, or bucket accessible to all anonymous internet users.

Each account supports only 1,000 ACLs. If this upper limit is exceeded, select bucket policies or user policies instead.

### When do I use a user policy?

If you want to specify what operations a user can perform, you are advised to configure user policy. You can search for a CAM user and check the permissions of the user's user groups to see what operations the user can perform. A user policy is recommended in scenarios where you want to:
- Configure COS service-level permissions such as the permissions for bucket creation and bucket listing.
- Grant permissions on all COS buckets and objects under your root account.
- Grant the same permissions to a large number of CAM users under the root account.

### When do I use a bucket policy?

If you want to specify which users can access a COS bucket, you are advised to configure a bucket policy. You can search for a bucket and check the bucket's policy to see who can access the bucket. A bucket policy is recommended in scenarios where you want to:
- Authorize a specific bucket.
- Authorize a specific action with the authorization effect set to `deny` or `allow`, which is not supported by ACL.
- Use cross-account authorization and anonymous user authorization, which are not supported by user policies.
