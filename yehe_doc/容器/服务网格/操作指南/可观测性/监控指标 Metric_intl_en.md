Currently, Tencent Cloud Mesh can choose to use [Managed Service for Prometheus (TMP)](https://intl.cloud.tencent.com/document/product/457/46734) to provide you with the collection, storage, and display of service traffic metric data.
>? Tencent Cloud Mesh will support the use of third-party Prometheus services as monitoring backend services in the near future.

Monitoring charts on the Tencent Cloud Mesh console will be displayed based on the monitoring metrics stored in TMP. If you have custom monitoring requirements, you can set a custom monitoring dashboard through the Grafana dashboard in TMP.

## Directions

Based on the metric data reported by sidecars to TMP, the Tencent Cloud Mesh console provides display and analysis of mesh topology, service topology, and service monitoring (number of requests, request status code distribution, request duration, and request size) charts.

### Enabling TMP Monitoring
On the [**Create mesh**](https://intl.cloud.tencent.com/document/product/1152/47461) page or the **Basic information** page of the mesh, find **Observability configuration** > **Monitoring metrics**, select **TMP**, and select **Automatic creation** or **Associate existing** for **TMP instance** as needed. After TMP monitoring is enabled, sidecars will report metric data to the corresponding instance, and you can view the instance on the TMP console.
![](https://qcloudimg.tencent-cloud.cn/raw/c4fff15bb91c0d7d3f0be894be99452a.png)

### Viewing Monitoring Charts
#### Mesh topology
A mesh topology records call structures of all services in a service mesh. Before viewing the mesh topology, ensure that sidecars have been injected into related services and that there is request traffic. The procedure of viewing the mesh topology of a specified mesh is as follows:
1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh), and click a specified mesh ID in the list to enter the mesh details page.
2. Click **Mesh topology** in the left sidebar, and view the mesh topology of the specified mesh.
![](https://qcloudimg.tencent-cloud.cn/raw/b0328f127b75c42aed61b66214fd69f8.png)
3. Click a node to display monitoring details related to the node. 
![](https://qcloudimg.tencent-cloud.cn/raw/ffd302ed7b7609ea74abc6640930a288.png)
4. At the top of the page, select data filtering conditions (including namespace and time span) and granularity of nodes (service granularity and workload granularity are supported currently).
![](https://qcloudimg.tencent-cloud.cn/raw/849fea2f7adb0d536280e2e2723a89c3.png)

#### Service topology
A service topology records dependencies between previous and next calls of a service. The procedure of viewing the service topology of a specified service is as follows:

1. On the details page of the specified mesh, click **Service** in the left sidebar to enter the service list page.
2. Click the service to be viewed to enter the service details page.
![](https://qcloudimg.tencent-cloud.cn/raw/1f8af0f1392674bfdf0194c364759b91.png)
3. On the **Basic information** tab page of the service details page, view the service topology of the service.
![](https://qcloudimg.tencent-cloud.cn/raw/ba62311715c82870dc425db3c4def890.png)

#### Service monitoring
You can compare the monitoring data (such as the number of requests, request duration, request size) of multiple services on the service list page, or view the monitoring details of a specified service on the service details page.

- Viewing the monitoring data of multiple services on the service list page
	1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh), and click a specified mesh ID in the list to enter the mesh details page.
	2. Choose **Service** > **Monitor**, click the service whose monitoring data is to be viewed, and view the service monitoring data on the right.
  ![](https://qcloudimg.tencent-cloud.cn/raw/6cadc6fa7f511e8f91ae119ec0968b48.png)



- Viewing the detailed monitoring data charts of a specified service on the service details page
 1. On the details page of the specified mesh, click **Service** in the left sidebar to enter the service list page.
 2. Click the service to be viewed to enter the service details page.
 3. View the charts on the **Monitor** tab page of the service details page.
![](https://qcloudimg.tencent-cloud.cn/raw/8d5d49b0b09f457a382fb5ae6e5a61fe.png)

### Disabling monitoring

You can choose to edit the observability configuration on the **Basic information** page of the mesh, and deselect **TMP**. After deselection, the TMP instance will not be deleted on the Tencent Cloud Mesh side. If necessary, go to the [TMP console](https://console.cloud.tencent.com/tke2/prometheus2/list?rid=4) to delete the TMP instance.
