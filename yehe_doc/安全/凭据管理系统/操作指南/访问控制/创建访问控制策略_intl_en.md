## Authorizable Resource Types
Resource-level permission refers to the capability to specify resources that an account can perform operations on. Some SSM APIs support operations on secrets using resource-level permissions. This can control when a user can perform operations and whether the user can use specific resources.
For example, if you allow a user to have access to secrets in the Guangzhou region, the authorizable resource type in CAM is as follows:
```
qcs::ssm:ap-guangzhou:uin/${uin}:*
qcs::ssm:ap-guangzhou::*
```
If you authorize an API to access all secrets created by a certain UIN, the resource type is as follows:
```
qcs::ssm:$region:uin/$uin:secret/creatorUin/*
```
If you authorize an API to access a certain secret, the resource type is as follows:
```
qcs::ssm:$region:uin/$uin:secret/creatorUin/$creatorUin/$secretName
```
Where,
- `$region`: region
-  `$uin`: root account ID
-   `$creatorUin`: account ID of the creator of the resource
-   `$secretName`: name of the secret that requires configuration

## Resource-level Authorization APIs
Resource paths of the `DeleteSecretVersion`, `UpdateDescription`, `RestoreSecret`, `EnableSecret`, `PutSecretValue`, `DescribeSecret`, `UpdateSecret`, `DeleteSecret`, `GetSecretValue`, `DisableSecret`, and `ListSecretVersionIds` APIs are as follows:
```
qcs::ssm:$region:uin/$uin:secret/*
qcs::ssm:$region:uin/$uin:secret/creatorUin/*
qcs::ssm:$region:uin/$uin:secret/creatorUin/$creatorUin/$secretName
```

## API-level Authorization List
| API | Description |
|---------|---------|
|CreateSecret|Creates a secret.|
|GetRegions|Obtains the list of available regions for displaying on the Console.|
|GetServiceStatus|Obtains the service status, which can be used to determine whether the service is activated.|
|ListSecrets|Obtains the information list of all secrets.|
