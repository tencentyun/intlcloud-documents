## Operation Scenario
This document shows how to quickly create a Node.js **Hello World** service in a container cluster. For more information on how to build a Docker image, please see [How to Build Docker Image](/doc/product/457/9115).

##  Prerequisites

- Create a cluster. For more information, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- Log in to node. This node has Node.js installed.

## Steps
### Writing Codes to Create an Image
### Write application
1. Execute the following commands in sequence to create and enter hellonode folder.
```shell
mkdir hellonode
cd hellonode/
```
2. Execute the following commands to create and open server.js file.
```
vim server.js
```
3. Press **i** or **Insert** to switch to editing mode, and enter the following contents into server.js.
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
Press **Esc** and enter **:wq** to save the file and return.
4. Execute the following commands to execute the server.js file.
```shell
node server.js
```
You can test the Hello World program in the following two ways.
 - Log in to the node again and execute the following commands.
```shell
curl 127.0.0.1:80
```
The following display indicates that the Hello World program is running successfully.
![](https://main.qcloudimg.com/raw/4b97b9e2fdaee77376b114ef92f90936.png)
 - Open the browser and access it by entering IP address:port. The port is 80.
 The following display indicates that the Hello World program is running successfully.
![](https://main.qcloudimg.com/raw/1fb82340313ab81dcffd693f9577624d.png)


#### Creating Docker Image
> For more information on docker images, see [How to Build a Docker Image](https://intl.cloud.tencent.com/document/product/457/9115).
>
1. Execute the following commands in sequence to create the Dockerfile file under the hellonode folder.
```
cd /hellonode
vim Dockerfile
```
2. Press **i** or **Insert** to switch to editing mode, and enter the following contents into the Dockerfile file.
```shell
FROM node:4.4
EXPOSE 80
COPY server.js .
CMD node server.js
```
Press **Esc** and enter **:wq** to save the file and return.
3. Execute the following commands to build the image.
```shell
docker build -t hello-node:v1 .
```
4. <span id="search">Execute the following command to view the hello-node image that was built.</span>
```
docker images 
```
The following display indicates that the hellonode image was successfully built. Note down its IMAGE ID. See the figure below:
![](https://main.qcloudimg.com/raw/d5bf4dfa0f805d6f90399c814b3152b1.png)


#### Uploading Image to Tencent Cloud Image Registry
>
>- Created the namespace in [My Images](https://console.cloud.tencent.com/tke2/registry/user/space).
>- Logged in to [Tencent Cloud Registry](https://intl.cloud.tencent.com/document/product/457/9117#.E7.99.BB.E5.BD.95.E5.88.B0.E8.85.BE.E8.AE.AF.E4.BA.91-registry). For more information on using images, see [Image Registry Basic Tutorial](https://intl.cloud.tencent.com/document/product/457/9117).

Execute the following commands in sequence to upload the image to the Tencent Cloud registry.
```shell
sudo docker tag IMAGEID ccr.ccs.tencentyun.com/namespace/helloworld:v1
sudo docker push ccr.ccs.tencentyun.com/namespace/helloworld:v1
```
>
>- Replace IMAGEID in the command with the IMAGEID noted down in [Step 4 above](#search).
>- Replace the namespace in the command with the namespace that you created.
>
The following display indicates that the image was successfully uploaded.
![](https://main.qcloudimg.com/raw/1aadc58e8663488200e3e34a532642c4.png)


### Creating Hello World Service Using This Image
> You must already have the following before creating and using the Hello World service:
>- A registered Tencent Cloud account. Go to the [Registration Page](https://intl.cloud.tencent.com/register) and fill out the related information to register a Tencent Cloud account.
>- Created a cluster. For more information, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
>
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
3. Click on the cluster ID for which the service is to be created, and go to the workload deployment details page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/bacaf92e14b7c342db6b3179c2ae5e8f.png)
4. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload Name**: Enter the name of the workload to be created. Here, helloworld is used as an example.
 - **Description**: Fill in the related workload information.
 - **Tag**: A “key = value” pair. In this example, the tag is “k8s-app = helloworld”.
 - **Namespace**: Select a namespace based on your requirements.
 - **Type**: Select a type based on your requirements.
 - **Volume**: Set up the workload volumes to mount based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
![](https://main.qcloudimg.com/raw/e2d083fececab9d1f84dd82f3850537a.png)
5. Set up **Containers in the pod**. Enter the pod container name. In this example, helloworld is used.
6. Click **Select Image** (keep other settings as default). See the figure below:
![](https://main.qcloudimg.com/raw/27b651e922b4a3afb925326ed8393bd0.png)
Select **My Images** from the pop-up box and find the helloworld image by using the search box feature. Click **OK**. See the figure below:
![](https://main.qcloudimg.com/raw/86a18f657b75d338ab3c084710c3ba10.png)
7. Set the number of pods. See the figure below:
 - **Manual Adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto Adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Service Auto Scaling](https://intl.cloud.tencent.com/document/product/457/14209).
 ![](https://main.qcloudimg.com/raw/6cc62e4c9118b83f7c4552a55f4c4cf0.png)
8. Set up the workload access settings according to the following instructions. See the figure below:   
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Via Internet**.
 - **Load Balancer**: Select according to your requirements.
 - **Port Mapping**: Select TCP protocol, and set both the container port and service port to 80.
 ![](https://main.qcloudimg.com/raw/57b97c8877fd3ac116c71fad4bf416f2.png)
 > You need to open this node and container network, Port 30000-32768 to Internet. Otherwise the container service will not be available. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
9. Click **Create Workload** to complete the creation of the HelloWorld service.

### Accessing HelloWorld Service
HelloWorld service can be accessed using the following two methods.
#### Accessing via Load Balancer IP
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the HelloWorld service’s cluster ID and select **Service** > **Service**.
3. Copy the Nginx service’s cloud load balancer IP from the service management page. See the figure below:
![](https://main.qcloudimg.com/raw/96fb6f94d4d365ce4007ff7961f5e438.png)
#### Access Using Service Name
Other services or containers in the cluster can be accessed directly by the service name.

### Verifying Hello World Service
When accessing the service, the following display indicates that the Hello World service was successfully created.
![](https://main.qcloudimg.com/raw/817c981526ac6297c778c1cb154a8d90.png)
If creation of the container failed, you can read the [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).
