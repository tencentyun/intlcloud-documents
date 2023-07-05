## Overview

This document describes how to create a simple web application through TKE.

A web application is divided into the following parts:
- The first part is the frontend service, which is used to handle query and write requests from clients.
- The other part is the data storage service, which uses Redis to store written data to redis-master and read data from redis-slave. Data is synchronized between redis-master and redis-slave through master-slave replication.

This application is a sample application supplied with the Kubernetes project. For more information, see the <a href="https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook">Guestbook App</a>.

## Prerequisites
- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/account/register).
- You have created a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions
### Creating a redis-master service
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the application is to be created. On the cluster details page that appears, select **Workload** > **Deployment** and click **Create**.
3. On the **Create Deployment** page, configure basic information of the workload. The main parameters are as follows. Retain the default settings for other parameters.
 - **Workload name**: **redis-master** is used as an example.
<dx-alert infotype="explain" title="">
For more information about the Deployment parameters, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662).
</dx-alert>
4. Configure **Containers in Pod** as instructed. The main parameters are as follows. Retain the default settings for other parameters.
 - **Name**: enter the name of the container in the pod. In this example, the name is **master**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/redis`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: in this example, you do not need to specify this field, but simply use the default policy.
5. Configure **Access Settings (Service)** for the workload as instructed below.
 - **Service**: select **Enable**.
 - **Service Access**: select **Intra-cluster**.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list and set both **Port** and **Target Port** to **6379**. In this way, other services can access the master container by using the “redis-master” service name and the 6379 port number.
6. Click **Create Deployment**.

### Creating a redis-slave service
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the application is to be created. On the cluster details page that appears, select **Workload** > **Deployment** and click **Create**.
3. On the **Create Deployment** page, configure basic information of the workload. The main parameters are as follows. Retain the default settings for other parameters.
 - **Workload Name**: indicates the name of the workload to be created. In this example, the name is **redis-slave**.
4. Configure **Containers in Pod** as instructed. The main parameters are as follows. Retain the default settings for other parameters.
 - **Name**: enter the name of the container in the pod. In this example, the name is **slave**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/gb-redisslave`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
 - **Environment Variable**: enter `GET_HOSTS_FROM = dns`.
5. Configure **Access Settings (Service)** for the workload as instructed below.
 - **Service**: select **Enable**.
 - **Service Access**: select **Intra-cluster**.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list and set both **Port** and **Target Port** to **6379**. In this way, other services can access the master container by using the “redis-master” service name and the 6379 port number.
7. Click **Create Deployment**.

### Creating a frontend service
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the application is to be created. On the cluster details page that appears, select **Workload** > **Deployment** and click **Create**.
3. On the **Create Deployment** page, configure basic information of the workload. The main parameters are as follows. Retain the default settings for other parameters.
 - **Workload Name**: the name of the workload to be created. In this example, the name is **frontend**.
4. Configure **Containers in Pod** as instructed. The main parameters are as follows. Retain the default settings for other parameters.
 - **Name**: enter the name of the container in the pod. In this example, the name is **frontend**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/gb-frontend`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
 - **Environment Variable**: enter `GET_HOSTS_FROM = dns`.
5. Configure **Access Settings (Service)** for the workload as instructed below.
 - **Service**: select **Enable**.
 - **Service Access**: select **Via Internet**.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list, and set both **Port** and **Target Port** to **80**. In this way, users can access the frontend container in a browser by using the load balancer IP address.
8. Click **Create Deployment**.


### Verifying the web application
1. Go to the cluster details page, and choose **Services and Routes** > **Service** in the left sidebar.
2. On the **Service** page, copy the load balancer IP address of the frontend service.
![](https://main.qcloudimg.com/raw/43d09b779fd2c0844b5c70d8ef373c53.png)
>?
>- You have selected the **Intra-cluster* access mode when creating the redis-master and redis-slave services. Therefore, these services have only one private IP address and can only be accessed by other services within the cluster.
>- You have selected the **Via Internet** access mode when creating the frontend service. Therefore, this service has a load balancer IP address (which is a public IP address) and a private IP address. As a result, this service not only can be accessed by other services in the cluster, but also can be accessed through the Internet.
>
4. Access the load balancer IP address of the frontend service in a browser. If the following page appears, the frontend service can be normally accessed.
![](https://main.qcloudimg.com/raw/d168ffa008a9c91e8b0e0c2051abd5a3.png)
5. Enter a random string in the field and click **Submit**. You will see that the entered string is saved and displayed at the bottom of the page.
Refresh the browser page to access the IP address of the service again. The previously entered string remains on the page, indicating that the string has been stored in Redis.

### Development practices
The following sample code is the complete code for the frontend service of the Guestbook app. When receiving an HTTP request, the frontend service determines whether it is a set command:
- If yes, the frontend service obtains the key and value from the parameters, connects to the redis-master service, and applies the key and value to the redis-master service.
- If no, the frontend service connects to the redis-slave service, obtains the value of the key parameter, and returns the value to the client to display.

```php
<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);
require 'Predis/Autoloader.php';
Predis\Autoloader::register();
if (isset($_GET['cmd']) === true) {
  $host = 'redis-master';
  if (getenv('GET_HOSTS_FROM') == 'env') {
    $host = getenv('REDIS_MASTER_SERVICE_HOST');
  }
  header('Content-Type: application/json');
  if ($_GET['cmd'] == 'set') {
    $client = new Predis\Client([
      'scheme' => 'tcp',
      'host'   => $host,
      'port'   => 6379,
    ]);
    $client->set($_GET['key'], $_GET['value']);
    print('{"message": "Updated"}');
  } else {
    $host = 'redis-slave';
    if (getenv('GET_HOSTS_FROM') == 'env') {
      $host = getenv('REDIS_SLAVE_SERVICE_HOST');
    }
    $client = new Predis\Client([
      'scheme' => 'tcp',
      'host'   => $host,
      'port'   => 6379,
    ]);
    $value = $client->get($_GET['key']);
    print('{"data": "' . $value . '"}');
  }
} else {
  phpinfo();
} ?>

```


### Notes

- When the frontend service accesses the redis-master and redis-slave services, it connects to the **Service name and port**. The cluster comes with the DNS service, which resolves the service name into the corresponding service IP address and performs load balancing according to this IP address.
Assume that the redis-slave service manages three pods. If the frontend service is directly connected to the redis-slave service and port 6379, the DNS service automatically resolves the redis-slave service into an IP address of the redis-slave service, which is a floating IP address similar to a load balancer IP address. Then, the DNS service automatically performs load balancing based on the IP address of the redis-slave service and sends a request to the corresponding pod of the redis-slave service.
- Note the following when specifying **Environment Variable** for the container:
 - **Default setting (recommended)**: during runtime, the frontend container reads the preset environment variable GET_HOSTS_FROM = dns and then directly connects to a service by using the service name.
 - **Other settings**: to obtain the domain name of the redis-master or redis-slave service, you must specify another environment variable.

