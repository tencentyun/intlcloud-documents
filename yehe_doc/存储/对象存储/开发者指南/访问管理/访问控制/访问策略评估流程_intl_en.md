Users should be authorized before they can get access to COS buckets and their resources. In the Tencent Cloud permissions system, a master account, by default, holds all management and administration permissions for the buckets and their resources. Without permission of the master account, such access will be denied for any CAM users (other root accounts, collaborators and sub-accounts), anonymous or any other type of users.

The types of access policies in an account include user group, user, bucket access control list (ACL), and bucket. As shown below, the evaluation of access policies depends on 3 key factors:

1. User authentication: When a user tries to access a resource in COS, either of the following two procedures applies:
	- If it is a signed request, COS parses the user account information out of it, and forwards the request to CAM for identity verification;
	- If it is an unsigned request, the user enters the next step of authentication as anonymous user.
2. Type of access policy, which includes user group, user, bucket, etc, and determines the order of an access policy.
3. Policy context: Whether a resource access request will succeed is finally determined based on the permission details recorded across the policies of all types including user group, user, and bucket.

## Access policy evaluation process

When Tencent Cloud COS receives a request, it first confirms the identity of the requester and verify that it has necessary permissions, including checking the user policy, bucket access policy, and resource-based ACL, and authenticating the request.

When COS receives a request, it first performs identity verification, the result of which determines the requester type. Different types may result in different actions:

1. Verified Tencent Cloud master account: A master account holds all operation permissions for the resources that it owns. For resources beyond those, the resource permissions should be evaluated, and the resource access will be permitted upon successful authentication.
2. Verified CAM user (sub-account or collaborator): needs evaluation of user policies. A CAM user must be authorized by its parent root account to be allowed to initiate an access. To access a resource in another root account, the CAM user should be evaluated for the resource permissions of its master account, and the resource access will be granted only upon successful authentication.
3. Unidentified anonymous user: needs evaluation of resource permissions, including permissions to access the policies or ACLs of buckets and objects in a bucket. The resource access will be granted upon successful authentication.
4. Access will be denied for any requesters other than the above types of users.

![Access Policy Evaluation Process](https://main.qcloudimg.com/raw/c4d2baea224306615f5d96209f26f520.png)

## How access policy evaluation works

In the Tencent Cloud permissions system, the access policy evaluation always occurs based on the policy context in the following basic principles:

1. By default, all requests are implicitly denied while a master account enjoys access permissions for all resources that it owns.
2. If an explicit allow exists in the user group/user/bucket policy, or bucket/object ACL, the above default is overridden.
3. An explicit deny overrides any allows in any policy.
4. The validity scope of permissions depends on the union of identity-based policies (user group/user policy) and resource-based policies (bucket policy or bucket/object ACL).


>
> - Explicit deny: is specified for certain users in the user/user group/bucket policy. For example, if a master account configures an explicit deny in its user policy targeted at a sub-user UIN 100000000011 who attempts to `GET Object`, this sub-user will be unable to download any resources in the master account.
> - Explicit allow: is specified for certain users in the user/user group/bucket policy or bucket ACL via `grant-\*`.
> - Deny anyone: is specified in the bucket policy. Once it is configured, any unsigned request will be denied while any signed request will be authenticated with identity-based policies.
> - Allow anyone: is specified in the bucket policy, or `public-\*` is specified instead in the bucket ACL.
> - The validity scope of permissions depends on the union of identity-based and resource-based policies. In a complete authentication, COS first parses the user identity, and then uses it to verify the resources the user has permissions to access. Besides, COS verifies the permissions of the user as anonymous user based on resource-based policies. Either verification is successful and the user will be allowed to access.

The following is a graphical illustration of access policy evaluation. First, evaluate if the requester is an anonymous user based on if the request carries a signature. For an anonymous user, continue to evaluate if Deny anyone or Allow anyone is specified in the policies and determine whether to allow or deny access based on the evaluation result. For a legitimate CAM user or a master account that owns the resource, evaluate if Deny, Allow, or Allow anyone is specified in the policies, and determine whether to allow or deny access based on the evaluation result.

![](https://main.qcloudimg.com/raw/1750209b6f01a998c185b0b209f2490b.png)

## Policy context

Policy context provides permission details recorded in your policies. Under the [principle of least privilege] (https://intl.cloud.tencent.com/document/product/436/32972), you should specify the following in your policies:

- principal: you should specify to which sub-account (user ID required), collaborator (user ID required), anonymous user, or user group to grant permission. This is not needed if you use a temporary key for access.
- statement: enter the corresponding parameters.
- effect: you must specify whether the policy is to "allow" or "deny".
- action: you must specify the allowed or denied operation. An operation can be an API (described using the prefix “name”) or a feature set (a set of specific APIs, described using the prefix “permid”).
- resource: you must specify the resource authorized by the policy. A resource is described in a six-piece format. You can set the resource scope as the specified file (e.g., `exampleobject.jpg`) or the specified directory (e.g., `examplePrefix/\*). Unless it is required by your business, please do not grant any user access to all resources using the `\*` wildcard.
- condition: it describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address.

You should write your policies following a certain policy syntax (See [Access Policy Language Overview]) (https://intl.cloud.tencent.com/document/product/436/18023) according to your business needs. For examples of writing user and bucket policies, see [Syntax Structure] (https://intl.cloud.tencent.com/document/product/598/10604) and [Examples of Bucket Policies] (https://intl.cloud.tencent.com/document/product/436/18031).

## Examples of access policy evaluation

Suppose that a master account UIN 100000000001 attaches a preset user policy to a sub-account UIN 100000000011, which allows the sub-account to read only the resources in the master account. With its details shown as below, this policy allows the sub-account to perform all `List`,` Get`, `Head`, and `OptionsObject` operations.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

Besides, the master account adds the following bucket policy to a bucket with private read/write `examplebucket-1250000000`:

```
{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::anyone:anyone"
        ]
      },
      "Effect": "Deny",
      "Action": [
        "name/cos:GetObject"
      ],
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/100000000011:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```

This bucket policy denies any users the ability to download objects (`GetObject`). Therefore, during the access policy evaluation:

1. If the sub-account requests to `GetObject` with a signature parameter, a user policy will be matched based on the requester identity indicated by the request, which will then be granted upon successful access policy evaluation and verification;
2. If the sub-account requests to `GetObject` without a signature parameter, it will be determined automatically as an anonymous requester, and **denied** access by the bucket policy.
