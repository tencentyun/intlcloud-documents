## Overview
This document describes how to quickly create a Node.js Hello World service in a container cluster. For more information on how to build a Docker image, see [How to Build a Docker Image](https://intl.cloud.tencent.com/document/product/457/9115).

## Prerequisites

- You have created a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have logged in to a node where Node.js has been installed.

## Steps
### Writing code to create an image
#### Developing an application
1. Run the following commands in sequence to create and go to the `hellonode` directory.
```shell
mkdir hellonode
```
```shell
cd hellonode/
```
2. Run the following command to create and open the `server.js` file.
```
vim server.js
```
3. Press i to switch to the editing mode, and copy the following code into `server.js`.
```js
var http = require('http');
var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!');
};
var www = http.createServer(handleRequest);
www.listen(80);
```
Press Esc and enter **:wq** to save the file and return.
4. Run the following commands to execute the server.js file.
```shell
node server.js
```
You can test the Hello World program in the following ways.
 - Log in to the node again and run the following command:
```shell
curl 127.0.0.1:80
```
If the following information appears, the Hello World program is running normally.
![](https://main.qcloudimg.com/raw/4b97b9e2fdaee77376b114ef92f90936.png)
 - Open a local browser and access the program by entering `<IP address>:<Port number>` in the address bar. Here, the port number is 80.
 If the following information appears, the Hello World program is running normally.
![](https://main.qcloudimg.com/raw/1fb82340313ab81dcffd693f9577624d.png)


#### Creating a Docker image
>?For more information on Docker images, see [How to Build a Docker Image](https://intl.cloud.tencent.com/document/product/457/9115).
>
1. Run the following commands in sequence to create a Dockerfile file in the `hellonode` directory.
```
cd hellonode
```
```
vim Dockerfile
```
2. Press i to switch to the editing mode, and copy the following code into the Dockerfile file.
```shell
FROM node:4.4
EXPOSE 80
COPY server.js .
CMD node server.js
```
Press Esc and enter **:wq** to save the file and return.
3. Run the following command to build the image.
```shell
docker build -t hello-node:v1 .
```
4. <span id="search">Run the following command to check the built hello-node image.</span>
```
docker images 
```
The hello-node image is successfully built if the following information appears. Note the IMAGE ID for future use, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d5bf4dfa0f805d6f90399c814b3152b1.png)


#### Uploading the image to the Tencent Cloud image registry
>!Prerequisites for uploading the image:
>- You have created a namespace in [My Images](https://console.cloud.tencent.com/tke2/registry/user/space).
>- You have logged in to [Tencent Cloud Registry](https://intl.cloud.tencent.com/document/product/457/9117). For more information on using images, see [Image Registry User Guide](https://intl.cloud.tencent.com/document/product/457/9117).

Run the following commands in sequence to upload the image to the Tencent Cloud image registry.
```shell
sudo docker tag IMAGEID ccr.ccs.tencentyun.com/<Namespace>/helloworld:v1
```
```
sudo docker push ccr.ccs.tencentyun.com/<Namespace>/helloworld:v1
```
>?
>- Replace IMAGEID in the command with the image ID mentioned in [Step 4](#search).
>- Replace the namespace in the command with the created namespace.
>
If the following information appears, the image was successfully uploaded.
![](https://main.qcloudimg.com/raw/1aadc58e8663488200e3e34a532642c4.png)


### Creating a Hello World service using the image
>!Before creating and using a Hello World service, ensure that:
>- You have registered a Tencent Cloud account. To do this, go to the [registration page](https://intl.cloud.tencent.com/register) and fill in the required information to register a Tencent Cloud account.
>- You have created a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
>
1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster on the "Cluster Management" page create the service and go to the workload "Deployment" page of the cluster. Then, click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/bacaf92e14b7c342db6b3179c2ae5e8f.png)
3. On the "Create Workload" page, specify the basic information of the workload as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/e2d083fececab9d1f84dd82f3850537a.png)
 - **Workload Name**: enter the name of the workload. In this example, the name is `helloworld`.
 - **Description**: specify the related workload information.
 - **Tag**: specify the key-value pair. In this example, the default is k8s-app = **helloworld**.
 - **Namespace**: select a namespace as required.
 - **Type**: select a type as required.
 - **Volume**: set the workload volume to mount. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure "Containers in Pod" as instructed. See the figure below.
Enter the name of the container. In this example, the name is `helloworld`.
![](https://main.qcloudimg.com/raw/27b651e922b4a3afb925326ed8393bd0.png)
Click **Select an image**, and click **My Images** in the dialog box that appears. Use the search box to find the helloworld image, and then click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/86a18f657b75d338ab3c084710c3ba10.png)
The following describes the main parameters:
 - **Image Tag**: use the default value `v1`.
 - **Image Pull Policy**: select one of the three available policies as required. In this example, the default policy is applied.
If you do not set any image pull policy and leave **Image Tag** empty or set it to `latest`, the `Always` policy is used. Otherwise, the `IfNotPresent` policy is used.
    - **Always**: always fetch the image remotely.
    - **IfNotPresent**: use a local image by default. Fetch the image remotely if no local image is available, 
    - **Never**: only use a local image. An exception occurs if no local image is available.
5. In the "Number of Pods" section, set the number of pods for the service as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/6cc62e4c9118b83f7c4552a55f4c4cf0.png)
 - **Manual adjustment**: specify the number of pods. In this example, it is set to 1. You can click "+" or "-" to change the number of pods.
 - **Auto Adjustment**: adjust the number of pods automatically when any of the set conditions is met. For more information, see [Automatic Scaling Basic Operations](https://intl.cloud.tencent.com/document/product/457/32424).
6. Configure **Access Settings (Service)** for the workload as instructed. See the figure below.   
![](https://main.qcloudimg.com/raw/57b97c8877fd3ac116c71fad4bf416f2.png)
 - **Service**: select "Enable".
 - **Service Access**: select "Public Network Access".
 - **Load Balancer**: create or select a load balancer as required.
 - **Port Mapping**: select the TCP protocol, and set both the container port and service port to port 80.
 >!The node network, container network, and ports 30000 to 32768 in the security group of the cluster that the service belongs to must be opened to Internet. Otherwise, TKE may be unavailable. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
7. Click **Create Workload** to create the Hello World service.

### Accessing the Hello World service
You can access the HelloWorld service with either methods.

#### Access with CLB IP address
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the "Cluster Management" page.
2. Click the ID of the cluster which the Hello World service belongs to and choose **Service** > **Service**.
3. On the service management page, copy the CLB IP address of the helloworld service, as shown in the following figure.
![](https://main.qcloudimg.com/raw/96fb6f94d4d365ce4007ff7961f5e438.png)

#### Access with service name
Other services or containers in the cluster can use the service name to directly access the Hello World service.

### Verifying the Hello World service
If the following information appears when you access the service, the Hello World service is successfully created.
![](https://main.qcloudimg.com/raw/817c981526ac6297c778c1cb154a8d90.png)
If the container cannot be created, you may search [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) for a solution.
