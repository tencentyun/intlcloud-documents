Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions, resources, and use permissions of your Tencent Cloud account. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

CAM operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------------|------|-----------------------------------|
| Adding sub-user with only console permissions                | cam  | AddConsoleUser                    |
| Adding user                    | cam  | AddSubAccount                     |
| Creating sub-user                   | cam  | AddSubAccountCheckingMFA          |
| Adding users to user group in batches                | cam  | AddSubAccountsToGroup             |
| Adding sub-user                   | cam  | AddUser                           |
| Adding user to user group                 | cam  | AddUserToGroup                    |
| Binding multiple policies to user group              | cam  | AttachGroupPolicies               |
| Binding policy to user group                | cam  | AttachGroupPolicy                 |
| Binding policy to multiple user groups              | cam  | AttachGroupsPolicy                |
| Binding multiple policies to role               | cam  | AttachRolePolicies                |
| Binding policy to role                 | cam  | AttachRolePolicy                  |
| Binding policy to multiple roles               | cam  | AttachRolesPolicy                 |
| Binding multiple policies to user               | cam  | AttachUserPolicies                |
| Binding policy to user                 | cam  | AttachUserPolicy                  |
| Binding policy to multiple users               | cam  | AttachUsersPolicy                 |
| Performing batch binding                    | cam  | BatchOperateCamStrategy           |
| Binding token                | cam  | BindToken                         |
| Checking sub-user name                 | cam  | CheckSubAccountName               |
| Querying whether the user is associated with any policies              | cam  | CheckUserPolicyAttachment         |
| Verifying custom MFA token           | cam  | ConsumeCustomMFAToken             |
| Creating access key                  | cam  | CreateAccessKey                   |
| Creating API key                 | cam  | CreateApiKey                      |
| Creating sub-account key                 | cam  | CreateCollApiKey                  |
| Creating user group                   | cam  | CreateGroup                       |
| Adding policy                    | cam  | CreatePolicy                      |
| CreatePolicyVersion     | cam  | CreatePolicyVersion               |
| Creating project key                  | cam  | CreateProjectKey                  |
| Creating role                    | cam  | CreateRole                        |
| Creating role in console                 | cam  | CreateRoleByConsole               |
| Creating SAML identity provider             | cam  | CreateSAMLProvider                |
| Creating sub-account binding limit               | cam  | CreateSubAccountBindPolicy        |
| Creating sub-account login IP policy             | cam  | CreateSubAccountLoginIpPolicy     |
| Adding user                    | cam  | CreateSubAccounts                 |
| Creating sub-account invitation QR code              | cam  | CreateSubUserInviteQRCode         |
| Deleting access key                  | cam  | DeleteAccessKey                   |
| Deleting API key                 | cam  | DeleteApiKey                      |
| Deleting sub-account key                 | cam  | DeleteCollApiKey                  |
| Deleting entity permission boundary                | cam  | DeleteEntitiesPermissionsBoundary |
| Deleting user group                   | cam  | DeleteGroup                       |
| Deleting policy                    | cam  | DeletePolicy                      |
| DeletePolicyVersion     | cam  | DeletePolicyVersion               |
| Deleting project key                  | cam  | DeleteProjectKey                  |
| Deleting role                    | cam  | DeleteRole                        |
| Deleting role permission boundary                | cam  | DeleteRolePermissionsBoundary     |
| Deleting SAML identity provider             | cam  | DeleteSAMLProvider                |
| Deleting user                    | cam  | DeleteSubAccount                  |
| Deleting sub-user                   | cam  | DeleteUser                        |
| Querying assisting approver                 | cam  | DescribeAssistApprover            |
| Getting policy details                  | cam  | DescribeCamStrategyDetail         |
| Getting role list                  | cam  | DescribeRoleList                  |
| Viewing sub-account binding limit               | cam  | DescribeSubAccountBindPolicy      |
| Viewing sub-account login IP policy             | cam  | DescribeSubAccountLoginIpPolicy   |
| Unbinding multiple policies from user group              | cam  | DetachGroupPolicies               |
| Unbinding policy from user group                | cam  | DetachGroupPolicy                 |
| Unbinding policy from multiple user groups              | cam  | DetachGroupsPolicy                |
| Unbinding multiple policies from role               | cam  | DetachRolePolicies                |
| Unbinding policy from role                 | cam  | DetachRolePolicy                  |
| Unbinding policy from multiple roles               | cam  | DetachRolesPolicy                 |
| Unbinding multiple policies from user               | cam  | DetachUserPolicies                |
| Unbinding policy from user                 | cam  | DetachUserPolicy                  |
| Unbinding policy from multiple users               | cam  | DetachUsersPolicy                 |
| Disabling API key                 | cam  | DisableApiKey                     |
| Deleting sub-account key                 | cam  | DisableCollApiKey                 |
| Disabling project key                  | cam  | DisableProjectKey                 |
| Enabling API key                 | cam  | EnableApiKey                      |
| Enabling sub-account key                 | cam  | EnableCollApiKey                  |
| Enabling project key                  | cam  | EnableProjectKey                  |
| Getting account summary                  | cam  | GetAccountSummary                 |
| Getting all sub-user information                | cam  | GetAllSubUser                     |
| Pulling API key                 | cam  | GetApiKey                         |
| Getting the association information of custom MFA token       | cam  | GetCustomMFATokenInfo             |
| Querying user group                   | cam  | GetGroup                          |
| Getting CAM password setting rule             | cam  | GetPasswordRules                  |
| Viewing policy details                  | cam  | GetPolicy                         |
| GetPolicyVersion        | cam  | GetPolicyVersion                  |
| Pulling project key                  | cam  | GetProjectKey                     |
| Getting role details                  | cam  | GetRole                           |
| Getting security settings overview information              | cam  | GetSafeAuthInfo                   |
| Querying the information of SAML identity provider           | cam  | GetSAMLProvider                   |
| Pulling sub-user binding information               | cam  | GetSubAccountBindInfo             |
| Pulling sub-user information                 | cam  | GetUser                           |
| Pulling basic user information                | cam  | GetUserBasicInfo                  |
| Listing access keys                  | cam  | ListAccessKeys                    |
| Querying policies associated with all user groups            | cam  | ListAllGroupsPolicies             |
| Viewing the list of policies associated with user group            | cam  | ListAttachedGroupPolicies         |
| Viewing the list of policies associated with role             | cam  | ListAttachedRolePolicies          |
| Listing all policies associated with user (including those associated with user group)       | cam  | ListAttachedUserAllPolicies       |
| Viewing the list of policies associated with user             | cam  | ListAttachedUserPolicies          |
| Viewing the list of entities associated with policy             | cam  | ListEntitiesForPolicy             |
| Getting user group list                 | cam  | ListGroups                        |
| Querying the list of user groups associated with user            | cam  | ListGroupsForUser                 |
| Querying the policies associated with user group in batches            | cam  | ListGroupsPolicies                |
| Querying identity provider list               | cam  | ListIdentityProvider              |
| Listing all policies                | cam  | ListPolicies                      |
| ListPolicyVersions      | cam  | ListPolicyVersions                |
| Getting message recipient list               | cam  | ListReceiver                      |
| Querying SAML identity provider list           | cam  | ListSAMLProviders                 |
| Getting user list                  | cam  | ListSubAccounts                   |
| Pulling sub-user list                 | cam  | ListUsers                         |
| Querying the list of users associated with user group            | cam  | ListUsersForGroup                 |
| Listing all users associated with policy (including those in associated user groups)     | cam  | ListUsersForPolicy                |
| Logging out role                 | cam  | LogoutRoleSessions                |
| Pulling the last login information                | cam  | LookupRecentlyLogin               |
| Passing role                    | cam  | PassRole                          |
| Setting entity permission boundary                | cam  | PutEntitiesPermissionsBoundary    |
| Setting role permission boundary                | cam  | PutRolePermissionsBoundary        |
| Pulling API key list               | cam  | QueryApiKey                       |
| Querying sub-account key list               | cam  | QueryCollApiKey                   |
| Pulling project key list                | cam  | QueryProjectKeyList               |
| Deleting user from user group                | cam  | RemoveUserFromGroup               |
| Sending sub-account information                 | cam  | SendSubAccountInfo                |
| SetDefaultPolicyVersion | cam  | SetDefaultPolicyVersion           |
| Setting security protection                  | cam  | SetSafeAuthFlag                   |
| Unbinding soft token               | cam  | UnbindStoken                      |
| Unbinding sub-user login method               | cam  | UnbindSubAccount                  |
| Updating access key                  | cam  | UpdateAccessKey                   |
| Updating role trust policy                | cam  | UpdateAssumeRolePolicy            |
| Updating policy                    | cam  | UpdateCamStrategy                 |
| Updating user group                   | cam  | UpdateGroup                       |
| Updating CAM password setting rule             | cam  | UpdatePasswordRules               |
| Modifying policy                    | cam  | UpdatePolicy                      |
| Modifying role login permission               | cam  | UpdateRoleConsoleLogin            |
| Updating role remarks                  | cam  | UpdateRoleDescription             |
| Updating SAML identity provider information           | cam  | UpdateSAMLProvider                |
| Updating user                    | cam  | UpdateSubAccount                  |
| Updating sub-account attribute                 | cam  | UpdateSubAccountAttr              |
| Updating sub-user                   | cam  | UpdateUser                        |
