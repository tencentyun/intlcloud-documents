## Operation Scenario

This article describes how to use Tencent Cloud TKE to construct a simple Web application.

Web applications are divided into the following parts.

- Frontend service, used to handle queries and write requests from clients.
- Data storage service, which uses redis to store data written into the storage to redis-master. By accessing redis-slave for read operations, redis-master and redis-slave ensure data synchronization through master-slave replication.
  This application is a built-in Kubernetes example, the URL is <a href="https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook">https://github.com/kubernetes/kubernetes/tree/release-1.6/examples/guestbook</a>.

## Directions

###Creating a Container Cluster

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke/cluster?rid=1)** to go to the cluster management page.
3. Click **[Create](https://console.cloud.tencent.com/tke/cluster/create?rid=1)** to go to the **Create a Cluster** page. This is shown in the following figure:
   ![Create a cluster](https://main.qcloudimg.com/raw/7cbdee82043ed142dc30962d0afbecdf.png)
4. Enter the following parameters according to actual requirements.

- Cluster Name: Custom.
- Project: Specify the project, and the newly added CVM, LoadBalancer, and other resources in the cluster will be automatically assigned to the project.
- Kubernetes Version: Specify the Kubernetes version.
- Region: Specify the location of the cluster.
- Cluster Network: Specify the node network for the cluster. The node network must be within a VPC. If you do not have one, [Create a VPC](https://console.cloud.tencent.com/vpc) first and create a subnet in this VPC.
- Container Network: Specify the container network. The IP of the containers in a cluster will be assigned from this network.

5. Click **Next**.
6. Select the Master method and payment mode of the cluster nodes according to actual requirements. Select the model, and configure the model, system disk, public network bandwidth,	
   etc. This is shown in the following figure:
   ![Select a model](https://main.qcloudimg.com/raw/ee04b24871660e87344df18ed223c6c7.png)
7. Click **Next**.
8. Select the operating system and security group according to actual requirements, and select the login method, configure a password, etc. This is shown in the following figure:
   ![CVM configuration](https://main.qcloudimg.com/raw/8f58c57764ccf3898036f059d85a885f.png)
9. Click **Next**.
10. Confirm the information, and click **Complete**. Wait several minutes for the creation to be completed successfully.

### Creating a Web Application

#### Creating redis-master Service

1. In the left sidebar, click **[Services](https://console.cloud.tencent.com/tke/service)** to go to the Service management page.
2. Click **[Create](https://console.cloud.tencent.com/tke/service/create)** to go to the **Create a Service** page.
3. Enter the following parameters, according to actual requirements. This is shown in the following figure:
   ![Create a Service](https://main.qcloudimg.com/raw/4214e8141c8d0dad79f12c924db12d27.png)

- Service Name: The name is `redis-master`.
- Region: Select the location of the cluster.
- Running Cluster: Select the newly created cluster.
- Running Container
  - Name: The name is `master`.
  - Image: Specify the `master` container image as `ccr.ccs.tencentyun.com/library/redis`.
  - Image tag: latest.
  - CPU/Memory limit: (Optional) Configure the CPU and memory resource limits.
- Number of Pods: Select **Manual adjustment**, and set it as 1.
- Service Access: Select **Intra-cluster**.
- Port mapping: Select TCP protocol, and set the service port and target port to 6379. Other services can access the `master` container by using the service name `redis-master` and port 6379.

4. Click **Create Service**.

#### Creating redis-slave Service

1. Click **[Create](https://console.cloud.tencent.com/tke/service/create)** to go to the **Service Creation** page.
2. Enter the following parameters, according to actual requirements. This is shown in the following figure:
   ![Create a Service](https://main.qcloudimg.com/raw/3050a6ea76a368745caa70bdcf8845f4.png)

- Service Name: The name is `redis-slave`.
- Region: Select the location of the cluster.
- Running Cluster: Select the newly created cluster.
- Running Container
  - Name: The name is `slave`.
  - Image: Specify the `master` container image as `ccr.ccs.tencentyun.com/library/gb-redisslave`.
  - Image tag: latest.
  - CPU/Memory limit: (Optional) Configure the CPU and memory resource limit.
  - Environment Variables: Add a name: GET_HOSTS_FROM, value: dns environment variable.
- Number of Pods: Select **Manual adjustment**, and set it as 1.
- Service Access: Select **Restrict access to within the cluster**.
- Port Mapping: Select TCP protocol, and set the service port and target port to 6379. Other services can access the `slave` container by using the Service name `redis-slave` and port 6379.

3. Click **Create Service**.

#### Creating a Frontend Service

1. Click **[Create](https://console.cloud.tencent.com/tke/service/create)** to go to the **Service Creation** page.
2. Enter the following parameters, according to actual requirements. This is shown in the following figure:
   ![Create a Service](https://main.qcloudimg.com/raw/f394092f104b00b91b3520846441152f.png)

- Service name: The name is `frontend`.
- Region: Select the location of the cluster.
- Running Cluster: Select the newly created cluster.
- Running Container
  - Name: The name is `frontend`.
  - Image: Specify the `master` container image as `ccr.ccs.tencentyun.com/library/gb-frontend`.
  - Image tag: latest.
  - CPU/Memory limit: (Optional) Configure the CPU and memory resource limit.
  - Environment variables: Add a name: GET_HOSTS_FROM, value: dns environment variable.
- Number of Pods: Select **Manual adjustment**, and set it as 1.
- Service Access: Select **Via Internet**.
- Port Mapping: Select TCP protocol. Set the Service port and target port as 80. The user can access the `frontend` container by using a browser to access the Cloud Load Balancer IP.

3. Click **Create Service**.

#### Viewing Services

In the left sidebar, click **[Services](https://console.cloud.tencent.com/tke/service)**, where you can see the three newly created Services. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/5e2bdd2ec19bc4224b93e71778ecbad2.png)

- When creating the `redis-master` and `redis-slave` Services, due to specifying the **Intra-cluster** access mode, the IP addresses of these two Services have only a private IP, and can only be accessed by other Services in the cluster.
- When creating the `frontend` Service, because the access mode **Via Internet** was set, this Service has one public IP (the public Cloud Load Balancer IP) and one private IP for internet access. As the access port of the `frontend` Service is 80, you can access the page by directly entering the public IP in the browser.
  The page shown below will appear, which means that you can access the `frontend` Service normally.
  ![](https://mc.qcloudimg.com/static/img/1d2bee6cf0a05db0e12d409cc83995b7/image.png)
  Enter any string in the input box, and you will see that the entered record has been saved, and is displayed at the bottom of the page. Close and reopen the browser, and re-enter the public IP address. The original data that was input still exists, which means that the input string has already been saved to `redis`.

### Development practices

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
  phpinfo ();
} ?>

```

This sample is the complete code for the `frontend` Service of Guestbook App. After `frontend` Service receives an HTTP request, it determines whether it is a `set` command.

- If it is a `set` command, it takes the `key` and `value` in the parameters, and links it to the `redis-master` service. It also sets the `key` and `value` to `redis-master`.
- If it is not a `set` command, it links it to the `redis-slave` Service, obtains the parameter `key` and corresponding value, and returns it to the client to display.

**Notes**:

1. `frontend` connects to the **Service name and port** when accessing the `redis-master` and `redis-slave` Services. The cluster comes with the DNS service, which resolves the service name into the corresponding service IP and performs load balancing according to this IP. Suppose the `redis-slave` service contains three Pods. When accessing this Service you actually connect to `redis-slave` and `6379`. The DNS automatically resolves `redis-slave` as the service IP of the `redis-slave` service (this is a floating IP, similar to a LoadBalancer IP) and automatically performs load balancing based on this IP, then sends the request to a `redis-slave` service Pod.
2. You can set environment variables for a container. In this example, when the `frontend` container runs, it reads the GET_HOSTS_FROM environment variable. If the variable value is `dns`, then the connection is made by using service name (recommended). Otherwise it must acquire the domain of `redis-master` or `redis-slave` from another environment variable.