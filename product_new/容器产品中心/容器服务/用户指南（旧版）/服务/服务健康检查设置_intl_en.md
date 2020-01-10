Tencent Cloud container cluster kernel supports periodic detection of the container based on kubernetes and kubernetes, which allows you to check the health status of the container and perform the following operations accordingly.

## Health Check Types
Heath check includes liveness check and readiness check. 
- **Liveness check**: it checks whether the container is alive, which is similar with checking whether a process exists via ps command. If the liveness check fails, the cluster will restart the container. No action is performed is the liveness check succeeds. 
- **Readiness check**: it checks whether the container is ready to process requests from the user. Some programs may need quite a long time to start up, such as it need to load data from disks or it’s relying on other external modules. In this case, the program process exists, but it’s not ready to provide service. The the readiness check fails, the cluster will not allow access to the container. If the check succeeds, the container will be open for access.

## Health Check Methods
### TCP Port Probe 
TCP port probe works as follows:
For containers providing TCP communication, the cluster periodically establishes TCP connection to test the connectivity. In this method, a container listening port must be specified. For example, for a Redis container with a service port of 6379, if you configure TCP port check for the container and specify the probe port to be 6379, then the cluster will periodically initiate a TCP connection to port 6379 of the container. The check succeeds if the connection is established, otherwise the check fails.

### HTTP Request Probe 
HTTP request probe is well suited for a container that provides HTTP/HTTPS services, where the cluster periodically initiates a HTTP/HTTPS GET request to the container. If the return code in the HTTP/HTTPS response is in the range of 200 - 399, the probe succeeds; otherwise, it fails.
For example, for a container that provides HTTP services with a service port of 80 and HTTP check path of `/health-check`, the cluster will periodically initiate a `GET http://containerIP:80/health-check` request to the container.

### Run Command Check ###
 is a powerful check method. After the user specify an executable command within the container, the cluster periodically executes the command in the container. If the result is 0, the check succeeds. Otherwise, the check fails.
Check by executing a command can be used as an alternative to TCP port probe and HTTP request probe:
-. For TCP port probe, a specific program is written to connect the port of the container. If the connection succeeds, the script returns 0; otherwise, it returns -1.
-. For HTTP request probe, a specific script is written to wget the container.
```wget http://127.0.0.1:80/health-check```
If the error code range of response is 200 - 399, the script returns 0; otherwise, it returns -1.

>**Note:** 
> - The program to be run must be placed in the image of the container; otherwise, the run will fail as the program cannot be found.
> - If the command to be run is a shell script, you cannot directly specify the script as the run command; instead, you need to add the script's interpreter. For example, if the script is `/data/scripts/health_check.sh`, the specified program should be `sh /data/scripts/health_check.sh` when run command check is used. 

## Other Common Parameters
- **Start-up Latency**: unit: second. It specifies the time before the probe starts after the container is started. For example, if the start delay is set to 5, then the health check will start 5 seconds after the container is started.
- **Interval**: unit: second. It specifies the frequency of health check. For example, if the interval is set to 10, then the cluster will be checked one every 10 seconds.
- **Response timeout**: unit: second. It indicates the TCP connection timeout period, the HTTP request response timeout period, and the run command timeout period for TCP port detection, HTTP request detection, and run command check, respectively.
- **Healthy Threshold**: unit: time. It specifies the times of consecutive health check successes before it is determined that the container is healthy. For example, if the healthy threshold is set to 3, the container will be considered healthy only if 3 consecutive probes succeed.
>**Note:** 
>If liveness check is selected, the **Healthy Threshold** can only be set to 1. This is because the container can be identified alive with only one successful probe.
- **Unhealthy Threshold**: unit: time. It specifies the times of consecutive health check failures before it is determined that the container is unhealthy. For example, if the unhealthy threshold is set to 3, the container will be considered unhealthy only if 3 consecutive probes fail.
