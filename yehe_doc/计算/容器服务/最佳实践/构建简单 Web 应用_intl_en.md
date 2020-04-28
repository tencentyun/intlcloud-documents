## Introduction

This document describes how to create a simple web application through TKE.

A web application is divided into the following parts:
- The first part is the frontend service, which is used to handle query and write requests from clients.
- The other part is the data storage service, which uses Redis to store written data to redis-master and read data from redis-slave. Data is synchronized between redis-master and redis-slave through master-slave replication.

This application is a sample application supplied with the Kubernetes project. For more information, see the <a href="https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook">Guestbook App</a>.

## Prerequisites
- You have registered a Tencent Cloud account. For more information, see [Registering a Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have created a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions
### Creating a redis-master service
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click on the cluster ID for which the application is to be created, and go to the Deployment page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/378d95d782c5efbf9cd9061f4c708e22.png)
3. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
![](https://main.qcloudimg.com/raw/ea0ddc2df9e0b2bcc826b852cd2c1805.png)
 - **Workload Name**: the name of the workload to create. In this example, it is set to “redis-master”.
 - **Description**: enter the information related to the workload.
 - **Label**: a key-value pair in the form of “key = value”. In this example, the default label is “k8s-app = redis-master”.
 - **Namespace**: select the value as required.
 - **Type**: select the value as required.
 - **Volume**: select the volume to which your workload will be mounted. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Set up **Containers in Pod** according to the following instructions. See the figure below:
![](https://main.qcloudimg.com/raw/3f7259f65a29fb5e782abb815a41835b.png)
The following describes the main parameters. For other parameters, simply leave them as their defaults.
 - **Name**: enter the name of the container in the pod. In this example, the name is **master**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/redis`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: three policies are available. Select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
If you do not specify the image pull policy, when the image tag is empty or "latest", the "Always" policy is used. Otherwise, the IfNotPresent policy is used.
    - **Always**: always fetch the image from the remote end
    - **IfNotPresent**: use the load image by default. If the local image is unavailable, fetch image from the remote end.
    - **Never**: only use local image. If the local image is unavailable, an exception occurs.
6. Set the number of pods.
![](https://main.qcloudimg.com/raw/5f861ae3fb55521d738a171764a3b097.png)
 - **Manual adjustment**: set the number of pods. In this example, the number of pods is 1. You can click the plus sign (**+**) or the minus sign (**-**) to adjust the number of pods.
 - **Auto adjustment**: the system automatically adjusts the number of pods if any specified condition is met. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/88d2188f7746184e88fe8a4375f0d5e1.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Intra-cluster**.
 - **Load Balancer**: select the value as required.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list and set both **Port** and **Target Port** to **6379**. In this way, other services can access the master container by using the “redis-master” service name and the 6379 port number.
8. Click **Create Workload** to finish creating the redis-master service.

### Creating a redis-slave service
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the service is to be created. On the **Deployment** page that appears, click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/3b828dcdb219b9466af30c359c505898.png)
3. On the **New Workload** page that appears, specify the basic information of the workload as instructed.
![](https://main.qcloudimg.com/raw/5d01db06dc78bc2136ce1b185af64dce.png)
 - **Workload Name**: indicates the name of the workload to be created. In this example, the name is **redis-slave**.
 - **Description**: enter the information related to the workload.
 - **Label**: indicates a key-value pair in the “key = value” format. In this example, the default label is “k8s-app = **redis-slave**”.
 - **Namespace**: select the value as required.
 - **Type**: select the value as required.
 - **Volume**: select the volume to which your workload will be mounted. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure the settings of **Containers in pod**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/16a69f993a1faf19399dcb45584de82e.png)
The following describes the main parameters. For other parameters, simply leave them as their defaults.
 - **Name**: enter the name of the container in the pod. In this example, the name is **slave**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/gb-redisslave`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
 - **Environment Variable**: enter the following configuration information:
GET_HOSTS_FROM = dns.
5. Set the number of pods.
![](https://main.qcloudimg.com/raw/10353f37e16c5e33a41bf71336ee93e7.png)
 - **Manual adjustment**: set the number of pods. In this example, the number of pods is 1. You can click the plus sign (**+**) or the minus sign (**-**) to adjust the number of pods.
 - **Auto adjustment**: the system automatically adjusts the number of pods if any specified condition is met. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
6. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/b7ce5914042e33b404fc87165e532afe.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Intra-cluster**.
 - **Load Balancer**: select the value as required.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list and set both **Port** and **Target Port** to **6379**. In this way, other services can access the slave container by using the redis-slave service name and the 6379 port number.
7. Click **Create Workload** to finish creating the redis-slave service.

### Creating a frontend service
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the application is to be created. On the **Deployment** page that appears, click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/46a7ea3299c791e8a31e4122a0f06b97.png)
3. On the **New Workload** page that appears, specify the basic information of the workload as instructed.
![](https://main.qcloudimg.com/raw/3c4b6d6277fe6f650ea464d1060e1ee6.png)
 - **Workload Name**: the name of the workload to be created. In this example, the name is **frontend**.
 - **Description**: enter the information related to the workload.
 - **Tag**: a key-value pair in the “key = value” format. In this example, we use "k8s-app = **frontend**".
 - **Namespace**: select the value as required.
 - **Type**: select the value as required.
 - **Volume**: select the volume to which your workload will be mounted. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
5. Configure the settings of **Containers in pod**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/0b5cfc640ced656bde9c782df01880d5.png)
The following describes the main parameters. For other parameters, simply leave them as their defaults.
 - **Name**: enter the name of the container in the pod. In this example, the name is **frontend**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/gb-frontend`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
 - **Environment Variable**: enter the following configuration information:
GET_HOSTS_FROM = dns.
6. Set the number of pods.
![](https://main.qcloudimg.com/raw/0e1dfb010735c93cca720b7e6fce0aa8.png)
 - **Manual adjustment**: set the number of pods. In this example, the number of pods is 1. You can click the plus sign (**+**) or the minus sign (**-**) to adjust the number of pods.
 - **Auto adjustment**: the system automatically adjusts the number of pods if any specified condition is met. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/c89da244015147adc6d11f21ceef9e8c.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Via Internet**.
 - **Load Balancer**: select the value as required.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list, and set both **Port** and **Target Port** to **80**. In this way, users can access the frontend container in a browser by using the load balancer IP address.
8. Click **Create Workload** to finish creating the frontend service.


### Verifying the web application
1. In the left sidebar, click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster where the created services are located. On the page that appears, choose **Services** > **Service**.
3. On the service management page, copy the load balancer IP address of the frontend service.
![](https://main.qcloudimg.com/raw/43d09b779fd2c0844b5c70d8ef373c53.png)
>
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

