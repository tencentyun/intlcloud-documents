## Overview
Cluster resources may be deleted or modified in the case of misoperations, application bugs, or apiserver API calls from malicious programs. You can use the cluster audit feature to keep logs of apiserver API calls. In this way, you can search and analyze audit logs to find the causes of problems. This document describes how to use the cluster audit feature for troubleshooting.



>! This document only applies to TKE clusters.

## Prerequisites
You have enabled the cluster audit feature in the TKE console. For more information, see [Enabling Cluster Audit](https://intl.cloud.tencent.com/document/product/457/38338#.E5.BC.80.E5.90.AF.E9.9B.86.E7.BE.A4.E5.AE.A1.E8.AE.A1).



## Use Case


### Obtaining the analysis result
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview?) and select **Search and Analysis** in the left sidebar.
2. On the **Search and Analysis** page, select the logset and log topic to search, and a time scope.
3. Enter the analysis statement and click **Search and Analysis** to obtain the analysis result.

### Example 1: querying the operator who cordoned a node
To query the operator who cordoned a node, run the following command:
```
objectRef.resource:nodes AND requestObject:unschedulable
```
On the **Search and Analysis** page, click **Layouts**. You can see the `user.username`, `requestObject`, and `objectRef.name` fields, which indicate the operator, request content, and node name, respectively. See the figure below:
![](https://main.qcloudimg.com/raw/ba803c37ab1335ebf0adc2675f8021cb.png)
As shown in the figure, the sub-account `10001****958` cordoned the `main.63u5qua9.0` node at `2020-10-09 16:13:22`. For more information on the sub-account, choose **Access Management** > **[User List](https://console.cloud.tencent.com/cam)** and click the account ID.


### Example 2: querying the operator who deleted a workload
To query the operator who deleted a workload, run the following command:
```
objectRef.resource:deployments AND objectRef.name:"nginx" AND verb:"delete" 
```
You can obtain detailed information about the subaccount based on the search result.
![](https://main.qcloudimg.com/raw/e42e024cc8e44298e332764305378e84.png)


### Example 3: locating the causes of apiserver access limitation

To prevent apiserver/etcd from being overloaded due to frequent apiserver access caused by malicious programs or bugs, apiserver enables an access limit mechanism by default. If the access limit is reached, you can identify the clients that have sent large numbers of requests through audit logs.
1. If you need to analyze clients that send requests based on userAgent, modify the log topic in the **Key Index** window and collect statistics based on the userAgent field, as shown in the figure below.
![](https://main.qcloudimg.com/raw/d8105a3a07ecf03666c93558c770557f.png)
2. Run the following command to collect QPS statistics from each client to the apiserver:

```java
* | SELECT CAST((__TIMESTAMP_US__ /1000-__TIMESTAMP_US__ /1000%1000) as TIMESTAMP) AS time, COUNT(1) AS qps,userAgent GROUP BY time,userAgent ORDER BY time
```
3. Switch to chart analysis and select line chart as the chart type. Select time as the X-axis, QPS as the Y-axis, and userAgent for the aggregation column, as shown in the figure below.
![](https://main.qcloudimg.com/raw/cfa2930a0fc145da0b668ff5bfe4d300.png)
After obtaining the data, click the data to add it to the dashboard for display, as shown in the figure below.
![](https://main.qcloudimg.com/raw/445363751f142ffff2c7e84b96f395ce.png)
The figure shows that the frequency of requests from the kube-state-metrics client to the apiserver is much higher than that of other clients.
According to the log, kube-state-metrics frequently sends requests to the apiserver due to RBAC permission issues. As a result, the apiserver access limit is triggered. The log is as follows:
```
I1009 13:13:09.760767       1 request.go:538] Throttling request took 1.393921018s, request: GET:https://172.16.252.1:443/api/v1/endpoints?limit=500&resourceVersion=1029843735
E1009 13:13:09.766106       1 reflector.go:156] pkg/mod/k8s.io/client-go@v0.0.0-20191109102209-3c0d1af94be5/tools/cache/reflector.go:108: Failed to list *v1.Endpoints: endpoints is forbidden: User "system:serviceaccount:monitoring:kube-state-metrics" cannot list resource "endpoints" in API group "" at the cluster scope
```
To use other fields, such as user.username, to distinguish the clients to collect data on, you can modify the SQL statement as required. An example SQL statement is as follows:
```
 * | SELECT CAST((__TIMESTAMP_US__ /1000-__TIMESTAMP_US__ /1000%1000) as TIMESTAMP) AS time, COUNT(1) AS qps,user.username GROUP BY time,user.username ORDER BY time
```
The following figure shows the display result.
![](https://main.qcloudimg.com/raw/dd1fbcc2efcc39ff3e9891ec3587a46f.png)



## References 
- For more information on the TKE cluster audit feature and basic operations, see [Cluster Audit](https://intl.cloud.tencent.com/document/product/457/38338).
- Cluster audit data is stored in Cloud Log Service (CLS). To search and analyze the audit results in the CLS console, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439) for the search syntax.
- To analyze audit data, an SQL statement supported by CLS is required. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/614/37803).
