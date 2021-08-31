Tencent Cloud Serverless Cloud Function (SCF) is a serverless execution environment provided for organizations and developers. It can help you run code with no need to purchase and manage servers, making it an ideal computing platform in scenarios such as real-time file processing and data processing. All you need to do is to write the core code using the languages supported by the platform and set the conditions for code execution. After that, your code can be executed on the Tencent Cloud infrastructure in an elastic and secure manner.

SCF operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|----------------------------------------------------|------|-------------------------------|
| Copying function                                               | scf  | CopyFunction                  |
| Creating function version alias                                           | scf  | CreateAlias                   |
| Creating function                                               | scf  | CreateFunction                |
| Creating function testing template                                           | scf  | CreateFunctionTestModel       |
| Creating namespace                                             | scf  | CreateNamespace               |
| Setting function trigger                                           | scf  | CreateTrigger                 |
| Deleting alias                                               | scf  | DeleteAlias                   |
| Deleting function                                               | scf  | DeleteFunction                |
| Deleting function testing template                                           | scf  | DeleteFunctionTestModel       |
| Deleting the specified version of specified layer (once deleted, a version cannot be associated with the function again, but will not affect other functions that are referencing this layer)         | scf  | DeleteLayerVersion            |
| Deleting namespace                                             | scf  | DeleteNamespace               |
| Deleting function trigger                                            | scf  | DeleteTrigger                 |
| Querying account quota                                             | scf  | GetAccount                    |
| Querying account quota                                             | scf  | GetAccountSettings            |
| Getting alias details                                           | scf  | GetAlias                      |
| Getting function details                                             | scf  | GetFunction                   |
| Getting the download address of function code                                        | scf  | GetFunctionAddress            |
| Getting function log                                             | scf  | GetFunctionLogs               |
| Getting the corresponding serverless application model of function                                  | scf  | GetFunctionSAM                |
| Getting function testing template                                           | scf  | GetFunctionTestModel          |
| Getting the total number of functions                                             | scf  | GetFunctionTotalNum           |
| Getting the number of function triggers                                           | scf  | GetFunctionUsageTriggerCount  |
| Getting layer version details, such as links for downloading files in layer                            | scf  | GetLayerVersion               |
| Getting monthly usage                                           | scf  | GetUserMonthUsage             |
| Getting yesterday's data                                          | scf  | GetUserYesterdayUsage         |
| Getting alias list                                             | scf  | ListAliases                   |
| Getting function list                                             | scf  | ListFunctions                 |
| Getting the list of function testing templates                                         | scf  | ListFunctionTestModels        |
| Returning the list of all layers, which contains the information of the latest version of each layer and can be used for filtering during runtime after adaptation             | scf  | ListLayers                    |
| Returning the information of all versions of specified layer                                      | scf  | ListLayerVersions             |
| Listing namespaces                                           | scf  | ListNamespaces                |
| Querying function version                                             | scf  | ListVersionByFunction         |
| Using specified ZIP file or COS object to create layer version (every time this API is called with the name of the same layer, a new version will be generated) | scf  | PublishLayerVersion           |
| scfPublishVersion                                  | scf  | PublishVersion                |
| Updating alias configuration                                            | scf  | UpdateAlias                   |
| Updating function code                                             | scf  | UpdateFunctionCode            |
| Updating function configuration                                             | scf  | UpdateFunctionConfiguration   |
| Incrementally updating function code                                           | scf  | UpdateFunctionIncrementalCode |
| Updating function testing template                                           | scf  | UpdateFunctionTestModel       |
| Updating namespace                                             | scf  | UpdateNamespace               |
| Updating trigger status                                            | scf  | UpdateTriggerStatus           |
