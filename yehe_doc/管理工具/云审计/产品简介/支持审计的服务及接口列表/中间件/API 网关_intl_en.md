Tencent Cloud API Gateway is an API hosting service that enables full lifecycle management of APIs, including creation, maintenance, release, operation, deactivation, etc. It can be used to encapsulate your business and open up your data, business logic, and functionality in a secure and reliable manner for integration with your own systems and connections with partner businesses.

API Gateway operations supported by CloudAudit are as shown below:



| Operation Name | Resource Type | Event Name |
| ------------------------- | -------- | ------------------------------------------ |
| Binding environment                  | apigw    | BindEnvironment                            |
| Binding key                  | apigw    | BindSecretIds                              |
| Binding sub-domain name                | apigw    | BindSubDomain                              |
| Creating API                  | apigw    | CreateApi                                  |
| Creating key                  | apigw    | CreateApiKey                               |
| Creating service                  | apigw    | CreateService                              |
| Creating usage plan              | apigw    | CreateUsagePlan                            |
| Deleting API                  | apigw    | DeleteApi                                  |
| Deleting key                  | apigw    | DeleteApiKey                               |
| Deleting IP policy              | apigw    | DeleteIPStrategy                           |
| Deleting service                  | apigw    | DeleteService                              |
| Deleting usage plan              | apigw    | DeleteUsagePlan                            |
| Downgrading usage plan              | apigw    | DemoteServiceUsagePlan                     |
| Getting API details             | apigw    | DescribeApi                                |
| Getting API environment policy         | apigw    | DescribeApiEnvironmentStrategy             |
| Getting API key details         | apigw    | DescribeApiKey                             |
| Getting key list              | apigw    | DescribeApiKeysStatus                      |
| Querying API list             | apigw    | DescribeApisStatus                         |
| Getting API usage plan         | apigw    | DescribeApiUsagePlan                       |
| Getting service details              | apigw    | DescribeService                            |
| Getting the uploaded data of service environment key monitoring | apigw    | DescribeServiceEnvironmentKeyMonitorUpload |
| Getting service environment list          | apigw    | DescribeServiceEnvironmentList             |
| Creating service release version          | apigw    | DescribeServiceReleaseVersion              |
| Querying service list              | apigw    | DescribeServicesStatus                     |
| Getting service sub-domain list        | apigw    | DescribeServiceSubDomains                  |
| Getting usage plan API key     | apigw    | DescribeUsagePlanSecretIds                 |
| Querying usage plant list          | apigw    | DescribeUsagePlansStatus                   |
| Disabling key                  | apigw    | DisableApiKey                              |
| Enabling key                  | apigw    | EnableApiKey                               |
| Generating API document             | apigw    | GenerateApiDocument                        |
| Modifying API                  | apigw    | ModifyApi                                  |
| Modifying IP policy              | apigw    | ModifyIPStrategy                           |
| Modifying service                  | apigw    | ModifyService                              |
| Modifying the configuration of service environment monitoring data upload      | apigw    | ModifyServiceEnvironmentKeyMonitorUpload   |
| Modifying service environment policy          | apigw    | ModifyServiceEnvironmentStrategy           |
| Modifying sub-domain name                | apigw    | ModifySubDomain                            |
| Modifying usage plan              | apigw    | ModifyUsagePlan                            |
| Publishing service                  | apigw    | ReleaseService                             |
| Debugging API                  | apigw    | RunApi                                     |
| Unbinding environment                  | apigw    | UnBindEnvironment                          |
| Unbinding key                  | apigw    | UnBindSecretIds                            |
| Unbinding sub-domain name                | apigw    | UnBindSubDomain                            |
| Deactivating environment                  | apigw    | UnReleaseService                           |
| Updating API key             | apigw    | UpdateApiKey                               |
| Modifying service                  | apigw    | UpdateService                              |