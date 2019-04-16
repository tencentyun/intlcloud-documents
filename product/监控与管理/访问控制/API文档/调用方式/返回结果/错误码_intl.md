## Feature Description

The error codes in the response indicate the result of the call to a cloud API.

- "code" stands for the common error code, which universally applies to the all API modules: 0 indicates a successful API call, while any other number suggests a failure. When the call fails, you can identify the cause of the error by looking up the list of common error code and take action accordingly.
- "codeDesc" stands for modular error code, which indicates a module-related errors. When the call fails, you can identify the cause of the error by looking up the list of module error code and take action accordingly.

## Error Codes

### Common error codes

| Error Code | Error Type | Description |
| -------- | ------------ | ------------------------------------------------------------ |
| 4000 | Invalid request parameter | Required parameter is missing, or parameter value is in an incorrect format. For error message, see the "message" field in error description. |
| 4100 | Authentication failed | Signature authentication failed. |
| 4200 | Request expired | Request has expired. |
| 4300 | Access denied | Account is blocked or is not within the user range for the API. |
| 4400 | Quota exceeded | The number of requests exceeded the quota limit. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact customer service. |
| 4500 | Replay attack | The use of Nonce and Timestamp can ensure that each request is executed only once on the server. Therefore, please make sure the current Nonce is different from the last one, and the difference between Timestamp and Tencent server time is less or equal than 2 hours. |
| 4600 | Unsupported protocol | Protocol is not supported. |
| 5100 | Failed to generate credential | An error occurred while generating a credential via API, which is a backend service error |

### Modular error codes

| Error Code | Modular Error Code (codeDesc) | Description | Action |
| ---- | ----------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 4000 | InvalidParameter.policyName.InUse | The policy name already exists. Policy name must be unique under the same account as required by CAM. | Use a new policy name. |
| 4000 | InvalidParameter | Invalid input parameter. | See the returned error message to check the appropriate parameter. |
| 5100 | InternalError | Internal system error | - |
| 4000 | InvalidParameter.AttachmentFull | The number of policies bound to user/user group/role has reached the upper limit. The maximum number of policies to be added to a user/user group/role is 200. Binding extra policies may fail. | Unbind some of the existing policies. |
| 4000 | InvalidParameter.principal.Error | The "principal" field in policy syntax is incorrect. | See the description of the [principal](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) field in the document. |
| 4000 | InvalidParameter.action.Error | The "action" field in policy syntax is incorrect. | See the description of [action](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in the document. |
| 4000 | InvalidParameter.effect.Error | The "effect" field in policy syntax is incorrect. | See the description of effect in the document. |
| 4000 | MissingParameter.action | The "action" field in policy syntax is missing. | Add [action](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in policy syntax. |
| 4000 | InvalidParameter.policyName.TypeError | The type of policy name is incorrect. Policy name must be a string. | Change the policy name to a string. |
| 4000 | InvalidParameter.policyName.Error | The policy name contains invalid characters or the length exceeds the limit. The maximum length of the policy name is 128 bytes. The policy name can only contain letters, numbers or special characters `+=,.@_-`. | Modify the policy according to the description. |
| 4000 | InvalidParameter.policyDocument.TypeError | The type of policy syntax is incorrect. | Change the policy name to a string. |
| 4000 | MissingParameter.version | The "version" field in policy syntax is missing. | Enter the [version](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) parameter. |
| 4000 | InvalidParameter.version.Error | The "version" field in policy syntax is incorrect. | Check whether the format of [version](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in policy syntax is correct. |
| 4000 | MissingParameter.statement | The "statement" field in policy syntax is missing. | Enter the [statement](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) parameter. |
| 4000 | InvalidParameter.statement.Error | The "statement" field in policy syntax is incorrect. | Check whether the format of [statement](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in policy syntax is correct. |
| 4000 | InvalidParameter.policyDocument.LengthOverlimit | The length of policy exceeds 4096 byte limit. 
| Reduce the length of policy. Split the policy into multiple policies if it is too long. |
| 4000 | InvalidParameter.condition.Error | The "condition" field in policy syntax is incorrect. | Check whether [condition](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in policy syntax is correct. |
| 4000 | MissingParameter.resource | The "resource" field in policy syntax is missing. | Enter the [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) parameter. |
| 4000 | InvalidParameter.resource.Error | The "resource" field in policy syntax is incorrect. | Check whether the format of [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in policy syntax is correct. |
| 4000 | InvalidParameter.resource.user.Error | The "resource" in policy syntax is not a resource under your account. | Enter the current primary account as the owner of [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) in policy syntax. |
| 4000 | InvalidParameter.description.LengthOverlimit | The length of policy description exceeds 300 byte limit. | Reduce the length of policy description. |
| 4000 | MissingParameter.policyName | The input parameter "policyName" is missing. | Enter the policyName parameter. |
| 4000 | MissingParameter.policyDocument | The input parameter "policyDocument" is missing. | Enter the policyDocument parameter. |
| 4000 | InvalidParameter.description.TypeError | The type of policy description is incorrect. Policy description must be a string. | Check the type of policy description. |
| 4000 | InvalidParameter.policyId.NotExist | Policy ID does not exist. | Enter the correct policy ID. |
| 4000 | MissingParameter.policyId | The input parameter "policyId" is missing. | Enter the policyId parameter. |
| 4000 | InvalidParameter.policyId.TypeError | The type of policy ID is incorrect. Policy ID must be a number. | Check the type of the policy ID. |
| 4000 | InvalidParameter.policyFull | The number of policies under this account reached the limit. The upper limit is 1,000. | Delete the policies that are no longer used. |
| 4000 | InvalidParameter.user.NotExist | User does not exist, or the user of field "principal" in policy syntax does not exist. | Check whether the corresponding user exists. |
| 4000 | InvalidParameter.group.NotExist | User group does not exist, or the user group of field "principal" in policy syntax does not exist. | Check whether the corresponding user group exists. |
| 4000 | InvalidParameter.role.NotExist | The role does not exist. | Create the corresponding role. |
| 4000 | InvalidParameter.roleName.TypeError | The type of role name is incorrect. Role name must be a string. | Check whether the type of role name is incorrect according to the description. |
| 4000 | InvalidParameter.roleName.Error | The role name contains invalid characters or the length exceeds the limit. The maximum length of the role name is 128 bytes. The policy name can only contain letters, numbers or `+=,.@_-`. | Check whether the role name is correct according to the description. |
| 4000 | InvalidParameter.roleFull | The number of roles owned by this account reached the limit. An account can have a maximum of 250 roles. | Delete the roles that are no longer used. |
| 4000 | InvalidParameter.roleName.InUse| The role name already exists. Role name must be unique under the same account. | Use a new role name, or delete the existing role of the same name. |
| 4000 | CanNotGetOwnerUin | User's OwnerUin cannot be obtained. | Check whether the account ID is correct. |
| 4000 | GetAppIdError | User's AppId cannot be obtained. | Check whether the account ID is correct. |
| 4000 | SetTimeOutOfTime | The validity period of the temporary credential set by the user exceeds the upper time limit. | For more information, see parameter description of specific API. |
| 4000 | StrategyInvalid | The policy information set for obtaining the temporary credential of federated identity is incorrect. | See "message". |

 

