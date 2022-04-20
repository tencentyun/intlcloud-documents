If you have multiple users of ASR operations, and they all share your Tencent Cloud account access key, you may face the following problems:

- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from maloperations due to the lack of user access control.

In this case, you can avoid the above problems by allowing different users to manage different services through sub-accounts. By default, sub-accounts don't have permissions to use ASR or relevant resources. Therefore, you need to create a policy to grant different permissions to sub-accounts.

Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions of your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603). For more information on how to use CAM policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

You can skip this section if you don't need to manage permissions to ASR resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

## Getting Started
A CAM policy must authorize or deny the use of one or more ASR operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or some resources for certain operations). A policy can also include the conditions set for the manipulated resources.

Some APIs of ASR use API-level permissions, for which you don't need to specify authorization for certain resources. Some other APIs use resource-level permissions, for which you can specify authorization for certain resources.

<table>
<tr>
<th>Basic policy structure</th>
<th><a href="https://intl.cloud.tencent.com/document/product/1118/43351">Policy Syntax</a></th>
</tr>
<tr>
<td>Operation definition in a policy</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1118/43351">ASR Operations</a></td>
</tr>
<tr>
<td>Resource definition in a policy</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1118/43351">ASR Resource Path</a></td>
</tr>
<tr>
<td>ASR authorization granularity</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1118/43350">Resource-Level Permissions Supported by ASR</a></td>
</tr>
</table>

