### How is Tencent Kubernetes Engine Distributed Cloud Center billed?
Tencent Kubernetes Engine Distributed Cloud Center is currently in beta. You can use it free of charge.


### Why can I only choose Guangzhou for the available regions?

Tencent Kubernetes Engine Distributed Cloud Center is based on the multi-cluster application governance project “Clusternet”. When you activate the service, the Hub Cluster is enabled automatically at the backend. Other registered Child Clusters will be managed through the Hub Cluster.
Tencent Kubernetes Engine Distributed Cloud Center is currently in beta. You can only enable the Hub Cluster in Guangzhou to manage your clusters deployed in other regions. If you want to enable the Hub Cluster in other regions, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).


### If I created an application (for example, a Deployment) and distributed it to multiple clusters. How can I check the status of the application?
You can enter the details page of the application and check the application status on the topology map. Also, you can click the “Instance management” tab and check the status of the application in each cluster.
There is a certain latency in the update of status information. If you want to check the details of Deployment application in a cluster, you can go to TKE -> Cluster.

### Can I configure multiple localization/globalization policies for an application?
No, because Tencent Kubernetes Engine Distributed Cloud Center is currently in beta. You can configure multiple localization/globalization policies for an application in the future.
