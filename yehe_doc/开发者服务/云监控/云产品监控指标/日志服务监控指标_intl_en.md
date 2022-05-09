

## Namespace

Namespace=QCE/CLS

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------- | ---------- | ---- | ------------ | ------------------------ |
| TrafficWrite        | Write traffic     | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| TrafficIndex        | Index traffic   | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| TrafficIntranetRead | Private network read traffic | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| TrafficInternetRead | Public network read traffic | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| TotalTrafficRead    | Total read traffic | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| StorageLog          | Log storage size | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| StorageIndex        | Index storage size | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| TotalStorage        | Total storage size   | MB   | uin, TopicId | 60s, 300s, 3600s, 86400s |
| Request             | Number of service requests | -   | uin, TopicId | 60s, 300s, 3600s, 86400s |



## Overview of Parameters in Each Dimension

| Parameter | Dimension | Description | Format |
| ------------------------------ | -------- | -------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | uin      | Dimension name of the account ID   | Enter a string-type dimension name: uin                                |
| Instances.N.Dimensions.0.Value | uin      | Specific account ID        | Enter an account ID, such as 10000xxx0827                           |
| Instances.N.Dimensions.1.Name  | TopicId  | Dimension name of the log topic ID | Enter a string-type dimension name: TopicId                            |
| Instances.N.Dimensions.1.Value | TopicId  | Specific log topic ID     | Enter a log topic ID, such as 4d1a2931-0038-4fb6-xxxx-bf29449e255a |

## Input Parameter Description

**To query the monitoring data of log topic metrics, use the following input parameters:**

&Namespace=QCE/CLS	
&Instances.N.Dimensions.0.Name=uin	
&Instances.N.Dimensions.0.Value=Specific account ID 
&Instances.N.Dimensions.1.Name=TopicId	
&Instances.N.Dimensions.1.Value=Specific log topic ID	 

