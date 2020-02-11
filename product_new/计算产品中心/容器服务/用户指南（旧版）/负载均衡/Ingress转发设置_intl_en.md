### Use Limits
Services with the access method disabled in clusters cannot use Ingress. The types of services that can use Ingress are as follows:
- Public network access
- VPC private network access

Ingress also supports load balancing. The backend container node of the load balancer needs to open the corresponding port. Services with public network access and VPC private network access have the host port opened by default. When forwarding is configured to the backend service, services with the access method as intra-cluster access cannot be added. You can update the access method of your service as needed.


You can use Ingress to set the access method of your service. The access method does not conflict with Ingress. You can get started in two ways, `internet --> Services` or `internet --> Ingress --> Services` as shown below:
![Alt text](https://main.qcloudimg.com/raw/67ffea725ff35dbcc218ad123bf73d69.png)

### Domain Names and Wildcards
A domain name must comply with both the rules for the public network load balancing domain names and the Kubernetes rules for Ingress domain names:
1. It supports regular expression with a length of 1-80 characters.
2. Other than regular expression, it also supports `a - z 0 - 9 . -`.

For domain names with wildcards, currently only `*.example.com` is supported, and only one `*` can be used in one domain name.

### Ingress Configuration Example

Create the backend services that need to use Ingress:
- hello service: port 80 is listened with the entry file in `/path_hello/index.html`.
- bye service: port 80 is listened with the entry file in `/path_bye/index.html`.

Create and configure Ingress by following the steps below:
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which you want to configure Ingress to go to the Deployment page. Click **Service** > **Ingress** on the left to go to the Ingress page. Click **Create** as shown below:
![](https://main.qcloudimg.com/raw/d8bee786541a87e18dcc594e2c1b4116.png)
3. Resolve your domain name to the VIP of the load balancer. For more information, please see [Quickly Adding Domain Name Resolution](https://cloud.tencent.com/document/product/302/3446).
In the example below, `www.qcloudccs.com` is resolved to sample load balancer.
4. Set the Ingress forwarding rules on the Ingress details page as shown below:
![](https://main.qcloudimg.com/raw/3aaaa2dc5bc361387af8f5e17ebe4f96.png)
Test the access results as shown below:
![Alt text](https://mc.qcloudimg.com/static/img/4160d18aad9fd9d0da7b69cabce9f2f9/%7BEF8EA5D8-4859-4008-9E3C-B98E7E25AAAF%7D.png)
![Alt text](https://mc.qcloudimg.com/static/img/47d9eca8fef9f7c492c4033d8080a0ae/%7B1700D9DE-417D-4F3E-8E9E-0883FA9A5C5C%7D.png)
