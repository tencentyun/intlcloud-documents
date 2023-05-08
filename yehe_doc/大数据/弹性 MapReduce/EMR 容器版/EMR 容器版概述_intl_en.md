<dx-alert infotype="explain" title="Unavailable for Purchase:">
The container-based EMR has been unavailable for purchase from March 10, 2023 for feature updates, and existing clusters are not affected. The new edition will be available for beta testing soon. Please stay tuned.
</dx-alert>
Container-based EMR offers a new way of deploying open-source big data components solely based on a container service. For example, you can deploy big data components to the cloud-native EKS and leverage its strengths in container application management to reduce the resource Ops costs and quickly create a cluster to run big data jobs.

## Deployments
EMR provides open-source big data component deployments on CVM or EKS to meet different user needs.
![](https://qcloudimg.tencent-cloud.cn/raw/b704b6f776a67d14991ce51638c0f487.png)

| Deployment | Description | 
|---------|---------|
| EMR on CVM<nobr>| EMR deploys the open-source big data components on CVM based on user needs and starts the installed services.<br>In addition, the EMR console allows for Ops operations on cluster and component services to facilitate big data job execution. | 
| Container-based EMR<nobr>| EMR deploys the big data components in the resources provided by EKS, and the component services run in the container.<br>You can run Spark jobs directly in the container cluster and associate them with RSS clusters to improve stability. | 

## Strengths

| Strength | Description | 
|---------|---------|	
| Reduced costs<nobr> | Container-based EMR is serverless and out-of-the-box with a high resource utilization. <br>Spark clusters automatically create Pod resources based on job needs and release them after the jobs end, saving costs. | 
| Easy Ops 	| Container-based EMR is deployed based on EKS, a fully managed Kubernetes service. In contrast to CVM, it can quickly recover abnormal component services. <br>Spark clusters automatically adjust Pod resources, simplifying node resource Ops. | 
| Elastic scaling| Container-based EMR allows you to adjust the number of containers. It relies on EKS's unlimited resources and proprietary lightweight virtualization technology. <br>It can implement the quick scaling of Pod resources to support jobs involving a large data volume. | 





