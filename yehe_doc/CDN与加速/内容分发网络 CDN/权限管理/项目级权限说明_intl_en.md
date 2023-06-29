## Creating Policies
If you need to grant different project-level permissions such as those for data query, purge and prefetch, and domain name management to different sub-accounts, you can create a policy as follows:
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and click **Policies** on the left sidebar.
2. Click **Create Custom Policy** and select **Create by Product Feature or Project Permission**:
![](https://main.qcloudimg.com/raw/725a31eb8e55f05e9d79bb217771a28e.png)
3. Enter the policy name as required and select **CDN** as the service type below:
![](https://main.qcloudimg.com/raw/c80cdb6c1961b8642151501d5cd62efb.png)
4. Enable the operation set to be authorized as needed and associate them with desired projects (the default project cannot be authorized). Then, associate them with sub-users:
![](https://main.qcloudimg.com/raw/9b0a24b97c25fa74a2f1c5bb1336ae52.png)

## Resource-Level and Project-Level
Currently, categories of operation sets and their corresponding OPEN API2.0 and OPEN API3.0 APIs are as shown below. Sub-users with operation set permissions can call a 2.0 or 3.0 API in the following list for any domain name in an authorized project:

| Permission Set              | API2.0                                                       | API3.0                                                       | Authorization Required |
| :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------- |
| Query usage data and statistics | DescribeCdnHostInfo DescribeCdnHostDetailedInfo GetCdnStatusCode<br/>GetCdnStatTop<br/>GetCdnProvIspDetailStat | DescribeCdnData DescribeOriginData<br/>ListTopData<br/>DescribeIpVisit | Yes           |
| Query domain name information          | GetHostInfoById<br/>GetHostInfoByHost                        | DescribeDomains<br/>DescribeDomainsConfig                    | Yes           |
| Query a CDN log download link | GenerateLogList<br/>GetCdnLogList                            | DescribeCdnDomainLogs                                        | Yes           |
| Add a domain name              | AddCdnHost                                                   | AddCdnDomain                                                 | Yes           |
| Launch/Deactivate a domain name       | OnlineHost OfflineHost                                       | StartCdnDomain<br/>StopCdnDomain                             | Yes           |
| Delete a domain name              | DeleteCdnHost                                                | DeleteCdnDomain                                              | Yes           |
| Modify domain name configuration          | UpdateCdnConfig                                              | UpdateDomainConfig                                           | Yes           |
| Purge and prefetch              | RefreshCdnDir<br/>RefreshCdnUrl<br/>GetCdnRefreshLog<br/>CdnPusherV2<br/>GetPushLogs<br/>CdnOverseaPushser | PurgeUrlsCache<br/>PurgePathCache<br/>DescribePurgeTasks<br/>PushUrlsCache<br/>DescribePushTasks | Yes           |
| Query service              | QueryCdnIp (no authorization required)                                       | DescribeCdnIp                                                | Yes           |

## Console Permissions
- View usage data and statistics: if **View usage data and statistics** is enabled in the policy and associated with a project, the sub-user can view the following modules in the console:
  - Overview page: data display module
  - Statistical analysis: real-time monitoring
  - Statistical analysis: data analysis
  - Data monitoring over the entire network
- Query domain name information: if the policy enables **Query domain name information** and is associated with a project, the sub-user can view the domain name list and detailed configuration information of the authorized project on the **Domain Name Management** page in the console.
- Query a CDN log download link: if the policy enables **Query a CDN log download link** and is associated with a project, the sub-user can query a log download link on the **Log Service** page in the console.
- Add a domain name: if the policy enables **Add a domain name** and is associated with a project, the sub-user can add a domain name to the specified project.
- Launch/deactivate a domain name: if the policy enables **Launch/deactivate a domain name** and is associated with a project, the sub-user can launch/deactivate an acceleration domain name in the specified project.
- Delete a domain name: if the policy enables **Delete a domain name** and is associated with a project, the sub-user can delete an acceleration domain name in the specified project. As only deactivated domain names can be deleted, if the sub-user wants to delete a launched domain name, they need to have the permission to **launch/deactivate a domain name**.
- Modify domain name configuration: if the policy enables **Modify domain name configuration** and is associated with a project, the sub-user can modify the configuration of an accelerated domain name in the specified project.
- Purge and prefetch: if **Purge and prefetch** is enabled in the policy and associated with a project, the sub-user can submit corresponding purge or prefetch (allowlist) tasks and query their execution status on the **Cache Purge** page.
