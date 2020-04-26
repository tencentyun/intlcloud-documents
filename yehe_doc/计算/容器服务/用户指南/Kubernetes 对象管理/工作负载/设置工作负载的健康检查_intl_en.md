Tencent Cloud container clusters use Kubernetes kernel. Kubernetes supports periodic container probes and uses the results from these probes to conclude container health status. Once you have the health status, you can proceed to perform additional operations.

## Health Check Types

These are the types of health checks:
- **Liveness**: this checks whether the container is alive, which is similar to checking whether a process exists using ps. If the check fails, the cluster will restart the container. No action is performed if the check succeeds.
- **Readiness check**: this checks whether the container is ready to handle user requests. For example, an application may take a long time to get ready because it need to mount a data volume or depends on an external module. In this case, you can use readiness check to make sure the application has finished loading. If the check fails, the cluster prevents requests from accessing the container. If the check is successful, the cluster allows access to the container.

## Health Check Methods

<span id="TCPPortProbe"></span>
### TCP port probe

TCP port probe works as follows:
The cluster attempts to establish a TCP connection to containers that provide TCP services periodically. If the connection is established, the probe is successful. Otherwise, the probe fails. To use TCP port probe, you must specify a listening port for the container.
For example, a container runs redis on port 6379 and a TCP probe is configured for the container on port 6379. The cluster will then attempt to establish a TCP connection with the container on port 6379 periodically. If the connection succeeds, the check has been successful. Otherwise, the check has failed.

<span id="HTTPRequestProbe"></span>
### HTTP request probe

HTTP request probe is suitable for containers that provide HTTP/HTTPS services. The cluster periodically initiates an HTTP/HTTPS GET request to the container. If the return code in the HTTP/HTTPS response is in the range of 200 - 399, the probe has succeeded; otherwise, it has failed. When HTTP request probe is used, be sure to specify the listening port and the HTTP/HTTPS request path.
For example, for a container that runs an HTTP service on port 80 with a health check path of `/health-check`, the cluster will periodically initiate a `GET http://containerIP:80/health-check` request on the container.

### Command probe

Command probe is a powerful way to perform health checks. It requires the user to specify an executable command in the container. The cluster periodically executes the command in the container. If the result is 0, the check has succeeded. Otherwise, the check has failed.
You can replace both [TCP port probe](#TCPPortProbe) and [HTTP request probe](#HTTPRequestProbe) by performing a command probe:
- To replace TCP port probes, write a script that tries to connect to a container port. If the connection succeeds, return 0; otherwise, return -1.
- To replace HTTP request probes, write a script that performs wget on the container and check the return code of the response. For example, `wget http://127.0.0.1:80/health-check`. If the return code is in the range of 200 - 399, return 0; otherwise, return -1.

#### Considerations
- Place the program in the image of the container; otherwise, the run will fail as the program cannot be found.
- You cannot specify the script as the command. Be sure to add the script interpreter. For example, if the script is `/data/scripts/health_check.sh`, use the following program to run the command:
```
sh 
/data/scripts/health_check.sh 
```
The following is an example of creating a Deployment using the [TKE Console](https://console.cloud.tencent.com/tke2):
 1. In the “Deployment” page of the cluster, click **Create””.
 2. Go to the **Create a Workload** page, select **Advanced Setting** below “Instances in a Container”.
 3. In “Container Health Check” page, set the following parameters.
 
   - **Probe**: select “Command probe”.
   - **Command**: enter the following:
   ```
sh 
/data/scripts/health_check.sh 
   ```
 - For other parameters, see [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).

## Other Common Parameters

- **Start-up Latency**: unit: second. It specifies the time before the probe starts after the container is started. For example, if the start-up latency is set to 5, then the health check will start 5 seconds after the container is started.
- **Interval**: unit: second. It specifies the frequency of the health check. For example, if the interval is set to 10, then the cluster will be checked once every 10 seconds.
- **Response timeout**: unit: second. It specifies the timeout period for the health check. It indicates the TCP connection timeout period, the HTTP request response timeout period, and the command timeout period for the TCP port probe, HTTP request probe, and command probe, respectively.
- **Health Threshold**: unit: time. It specifies the number of consecutive health check successes before a container is determined to be healthy. For example, if the health threshold is set to 3, the container will be considered healthy only if the probe succeeds 3 times in a row.
> If the type of health check is a liveness check, then the healthy threshold can only be 1. All other values are invalid.
- **Unhealthy Threshold**: unit: time. It specifies the number of consecutive health check failures before it is determined that the container is unhealthy. For example, if the unhealthy threshold is set to 3, the container will be considered unhealthy only if the probe fails 3 times in a row.
