The Tencent Cloud TKE kernel is based on Kubernetes, which periodic probes containers. It then uses the results to decide the health status of the containers and perform actions if needed.

## Health Check Types

Health checks are divided into the following types:
- **Liveness check**: it checks whether the container is alive, which is similar to checking whether a process exists using ps. If the liveness check fails, the cluster will restart the container. No action is performed if the liveness check succeeds.
- **Readiness check**: it checks whether the container is ready to handle user requests. For example, if an application takes a while to start up because it relies on a data disk mount or an external module startup to provide service, Kubernetes will use a readiness probe to check if the application has finished starting. If the readiness probe fails, requests to that container are blocked until the readiness probe succeeds. 

## Health Check Methods

<span id="TCPPortProbe"></span>
### TCP port probes

TCP port probe works as follows:
The cluster periodically tries to establish TCP connections to containers that provide TCP services. If the connection is established, the probe is successful. Otherwise, the probe fails. For TCP probes to work, you must specify the listening port of the container.
For example, you have a Redis service running on port 6379 and a TCP probe is set up to examine port 6379. The cluster will periodically try to establish a TCP connection to the container on port 6379. If the connection is established, the probe succeeds. If not, the probe fails.

<span id="HTTPRequestProbe"></span>
### HTTP request probes

HTTP request probes are for containers that provide HTTP/HTTPS services, where the cluster periodically initiates HTTP/HTTPS GET requests to the containers. If the return code of the HTTP/HTTPS response is in the range of 200 - 399, the probe succeeds; otherwise, it fails. When the HTTP request probe is used, be sure to specify the listening port and the HTTP/HTTPS request path.
For example, for a container that provides HTTP services with a service port of 80 and HTTP check path of `/health-check`, the cluster will periodically initiate a `GET http://containerIP:80/health-check` request to the container.

### Execute command check

It is a powerful check method. After the user specifies an executable command within the container, the cluster periodically executes the command. If the result is 0, the check succeeds. Otherwise, the check fails.
You can replace both [TCP port probes](#TCPPortProbe) and [HTTP request probes](#HTTPRequestProbe) with execute command checks:
- To replace TCP port probes, you can write a specific program to connect to a port of a container. If the connection succeeds, the script returns 0; otherwise, it returns -1.
- To replace HTTP request probes, you can write a script to execute wget to retrieve content from the container and check the return code of the response. For example, `wget http://127.0.0.1:80/health-check`. If the return code is in the range of 200 - 399, the script returns 0; otherwise, it returns -1.

#### Considerations
- The program to be run must be part of the image of the container. Otherwise, the execute command check will fail because the program cannot be found.
- If the execute command check uses a shell script, you cannot use the script as the command. Use a script interpreter to perform the check. For example, if the script is `/data/scripts/health_check.sh`, use the following:
```
sh 
/data/scripts/health_check.sh 
```
The following shows how to set up health checks using the [TKE Console](https://console.cloud.tencent.com/tke2):
 1. In the **Deployment** page of the cluster, click **Create**. The **CreateWorkload** page appears.
 2. Select **Advanced Settings** in the **Containers in a pod** section.
  3. Select **Liveness Check** for **Container Health Check** and configure the following parameters:
   - **Checking Method**: select **Execute Command Check**.
   - **Execute Command**: enter the following:
   ```
sh 
/data/scripts/health_check.sh 
   ```
 4. For other parameters, refer to [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).

## Other Common Parameters

- **Start-up Latency**: unit: seconds. This specifies the time to wait before starting a probe after a container is launched. For example, if the start delay is set to 5, the health check will start 5 seconds after the container is launched.
- **Interval**: unit: second. It specifies the frequency of health checks. For example, if the interval is set to 10, then health checks are run once every 10 seconds.
- **Response timeout**: unit: second. It specifies the timeout period for health check. It indicates the TCP connection timeout period, the HTTP request response timeout period, and the execute command timeout period for TCP port probe, HTTP request probe, and execute command check, respectively.
- **Healthy Threshold**: unit: time. It specifies the times of consecutive health check successes before the container is determined to be healthy. For example, if the healthy threshold is set to 3, the container will be considered healthy only if the probe succeeds three times consecutively.
>! For liveness checks, the healthy threshold can only be 1. Other values are invalid.
- **Unhealthy Threshold**: unit: time. It specifies the times of consecutive health check failures before the container is determined to be unhealthy. For example, if the unhealthy threshold is set to 3, the container will be considered unhealthy only if the probe fails three times consecutively.
