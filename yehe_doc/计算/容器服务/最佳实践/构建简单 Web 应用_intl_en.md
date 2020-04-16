## Operation Scenario

This document describes how to create a simple web application through TKE.

A web application is divided into the following parts:
- The first part is the frontend service, which is used to handle query and write requests from clients.
- The other part is the data storage service, which uses Redis to store written data to redis-master and read data from redis-slave. Data is synchronized between redis-master and redis-slave through master-slave replication.

This application is a sample application supplied with the Kubernetes project. For more information, see the <a href="https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook">Guestbook App</a>.

## Prerequisites
- You have registered a Tencent Cloud account. For more information, see [Registering a Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have created a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Procedure
### Creating a redis-master service
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the application is to be created. On the **Deployment** page that appears, click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/0192e80bccd66947eb505a18b4b536d4.png)
3. On the **New Workload** page that appears, specify the basic information of the workload as instructed.
![](https://main.qcloudimg.com/raw/f5a78647faa6096d81c682a271cc6aaf.png)
 - **Workload Name**: indicates the name of the workload to be created. In this example, the name is **redis-master**.
 - **Description**: enter the information related to the workload.
 - **Label**: indicates a key-value pair in the key = value format. In this example, the default label is k8s-app = **redis-master**.
 - **Namespace**: select the value as required.
 - **Type**: select the value as required.
 - **Volume**: select the volume to which your workload will be mounted. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure the settings of **Containers in pod**, as shown in the following figure.
![img](https://main.qcloudimg.com/raw/2a0c5b6a04d1458852d72eaa990712d7.png)
The following describes the main parameters. For other parameters, simply leave them as their defaults.
 - **Name**: enter the name of the container in the pod. In this example, the name is **master**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/redis`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: three policies are available. Select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
If you do not specify the image pull policy and the image tag is empty or latest, the Always policy is used. Otherwise, the IfNotPresent policy is used.
    - **Always**: indicates that the image is always fetched remotely.
    - **IfNotPresent**: indicates that the image is fetched locally by default. If the image is locally unavailable, the image is fetched remotely.
    - **Never**: indicates that the image is always fetched locally. If the image is locally unavailable, an exception occurs.
6. Set the number of pods.
![](![img](https://main.qcloudimg.com/raw/2abbedb170db5b366ab71351acde984c.png)
 - **Manual adjustment**: set the number of pods. In this example, the number of pods is 1. You can click the plus sign (**+**) or the minus sign (**-**) to adjust the number of pods.
 - **Auto adjustment**: the system automatically adjusts the number of pods if any specified condition is met. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/14209).
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/a70f48545734627844d495fd442985fa.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Intra-cluster**.
 - **Load Balancer**: select the value as required.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list and set both **Port** and **Target Port** to **6379**. In this way, other services can access the master container by using the redis-master service name and the 6379 port number.
8. Click **Create Workload** to finish creating the redis-master service.

### Creating a redis-slave service
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the service is to be created. On the **Deployment** page that appears, click **Create**, as shown in the following figure.
![](![img](https://main.qcloudimg.com/raw/e2430aa20d9215dec7a9cec2b711f3dd.png)
3. On the **New Workload** page that appears, specify the basic information of the workload as instructed.
![](https://main.qcloudimg.com/raw/81d945370bc248f6cec62a1674080895.png)
 - **Workload Name**: indicates the name of the workload to be created. In this example, the name is **redis-slave**.
 - **Description**: enter the information related to the workload.
 - **Label**: indicates a key-value pair in the key = value format. In this example, the default label is k8s-app = **redis-slave**.
 - **Namespace**: select the value as required.
 - **Type**: select the value as required.
 - **Volume**: select the volume to which your workload will be mounted. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure the settings of **Containers in pod**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/b4c0c7bffc64bc9bb35a9329ff88810f.png)
The following describes the main parameters. For other parameters, simply leave them as their defaults.
 - **Name**: enter the name of the container in the pod. In this example, the name is **slave**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/gb-redisslave`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
 - **Environment Variable**: enter the following configuration information:
GET_HOSTS_FROM = dns.
5. Set the number of pods.
![](https://main.qcloudimg.com/raw/8f3f5be325ce11f1c6c2a6ca523386b6.png)
 - **Manual adjustment**: set the number of pods. In this example, the number of pods is 1. You can click the plus sign (**+**) or the minus sign (**-**) to adjust the number of pods.
 - **Auto adjustment**: the system automatically adjusts the number of pods if any specified condition is met. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/14209).
6. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/05e2b80d381dd61ae7ba1d5dc53621eb.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Intra-cluster**.
 - **Load Balancer**: select the value as required.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list and set both **Port** and **Target Port** to **6379**. In this way, other services can access the slave container by using the redis-slave service name and the 6379 port number.
7. Click **Create Workload** to finish creating the redis-slave service.

### Creating a frontend service
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the application is to be created. On the **Deployment** page that appears, click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f2925b954bf4229e910d0b204f168aa0.png)
3. On the **New Workload** page that appears, specify the basic information of the workload as instructed.
![](https://main.qcloudimg.com/raw/f923b03293b8cda5145bdd5daf7b2f9d.png)
 - **Workload Name**: indicates the name of the workload to be created. In this example, the name is **frontend**.
 - **Description**: enter the information related to the workload.
 - **Tag**: indicates a key-value pair in the key = value format. In this example, the default label is k8s-app = **frontend**.
 - **Namespace**: select the value as required.
 - **Type**: select the value as required.
 - **Volume**: select the volume to which your workload will be mounted. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
5. Configure the settings of **Containers in pod**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/30218adc64d1a80b8296d050725b96ba.png)
The following describes the main parameters. For other parameters, simply leave them as their defaults.
 - **Name**: enter the name of the container in the pod. In this example, the name is **frontend**.
 - **Image**: enter `ccr.ccs.tencentyun.com/library/gb-frontend`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: select the value as required. In this example, you do not need to specify this field, but simply use the default policy.
 - **Environment Variable**: enter the following configuration information:
GET_HOSTS_FROM = dns.
6. Set the number of pods.
![](https://main.qcloudimg.com/raw/a7253584191db8dc28ddec7ef0abf992.png)
 - **Manual adjustment**: set the number of pods. In this example, the number of pods is 1. You can click the plus sign (**+**) or the minus sign (**-**) to adjust the number of pods.
 - **Auto adjustment**: the system automatically adjusts the number of pods if any specified condition is met. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/14209).
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/681d60e7a3a3100f1c054054406b4b11.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Via Internet**.
 - **Load Balancer**: select the value as required.
 - **Port Mapping**: select **TCP** from the **Protocol** drop-down list, and set both **Port** and **Target Port** to **80**. In this way, users can access the frontend container in a browser by using the load balancer IP address.
8. Click **Create Workload** to finish creating the frontend service.


### Verifying the web application
1. In the left sidebar, click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster where the created services are located. On the page that appears, choose **Services** > **Service**.
3. On the service management page, copy the load balancer IP address of the frontend service.
![](https://main.qcloudimg.com/raw/74be16e7d6cd0ec6ec310a9430519090.png)
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

- When the frontend service accesses the redis-master and redis-slave services, it connects to the **Service name and port**. The cluster comes with the DNS service, which resolves the service name into the corresponding service IP address and performs cloud load balancing according to this IP address.
Assume that the redis-slave service manages three pods. If the frontend service is directly connected to the redis-slave service and port 6379, the DNS service automatically resolves the redis-slave service into an IP address of the redis-slave service, which is a floating IP address similar to a load balancer IP address. Then, the DNS service automatically performs load balancing based on the IP address of the redis-slave service and sends a request to the corresponding pod of the redis-slave service.
- Note the following when specifying **Environment Variable** for the container:
 - **Default setting (recommended)**: during runtime, the frontend container reads the preset environment variable GET_HOSTS_FROM = dns and then directly connects to a service by using the service name.
 - **Other settings**: to obtain the domain name of the redis-master or redis-slave service, you must specify another environment variable.

