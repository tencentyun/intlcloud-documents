The method for accessing a service determines the network attribute of this service. Different access methods offer different network capabilities. Tencent Cloud TKE provides four service access methods: Access from Public Network, Access Within Cluster Only, Access via Private Network in VPC and Not Enabled.

## Access from Public Network
For services accessed from public network, an entry (the public network load balancer) for Internet access is provided. The service accessed using this method can be accessed directly from the public network. This method is applicable to Web frontend services, such as wordpress frontend service.
For example, if we create a wordpress service that can be accessed from public network, the service access method is set to **Access From Public Network**. The created service can be accessed directly through **LB IP + Service Port**.
![](https://main.qcloudimg.com/raw/2bee0bd98206821be4bf608beb4a08c5.png)
For more information on how to create a wordpress service, please see [WordPress with Single Pod](https://intl.cloud.tencent.com/document/product/457/7205).

## Access Within Cluster Only
For services accessed within a cluster, an entry (service IP) of being accessed by other services or containers within the cluster is provided. This method is applicable to MySQL and other database services to ensure the isolation among service networks.
For example, if we create a MySQL service that can be accessed within a cluster only, the service access method is set to **Access Within Cluster Only**. The created service can be accessed directly through **Service IP/Name + Service Port**.
![](https://main.qcloudimg.com/raw/bccd987374e809e7747b93ef641778a8.png)

## Access via Private Network in VPC
For services accessed via the private network in a VPC, an entry (private network load balancer) of being accessed by other resources under the VPC in which the cluster resides is provided. This method is applicable to services that need to be accessed by other clusters or CVMs under the same VPC.
For example, if we create a MySQL service that can be accessed via the private network in a VPC, the service access method is set to **Access via Private Network in VPC**. The created service can be accessed directly through **Private network LB IP + Service Port**.
![](https://main.qcloudimg.com/raw/c6a5f1ab032972297807277231d3480e.png)

## Not Enabled
If "Not Enabled" is selected for service access, no entry is provided for accessing from frontend service to the container. This can be used to discover or easily enable multiple container pods with custom service.

## More
In addition to the above four methods, you can also configure a layer-7 load balancer (HTTP/HTTPS) to forward to the service. For more information, please see [Ingress Forwarding Configuration](https://intl.cloud.tencent.com/document/product/457/9111).

