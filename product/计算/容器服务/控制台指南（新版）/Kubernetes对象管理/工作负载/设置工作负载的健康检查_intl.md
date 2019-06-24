TKE container cluster kernel is based on Kubernetes. Kubernetes supports periodic detection of containers and determines the health of the containers based on the results of the detection to perform additional operations.

## Health Check Types

Health checks are divided into the following types:
- **Container survival check**: Used to detect whether a container is alive, similar to running the ps command to check whether a process exists. If the container's survival check fails, the cluster will perform a restart operation on the container. If the container's survival check succeeds, no operations will be performed.
- **Container readiness check**: Used to detect whether a container is ready to begin processing user requests. For example, the startup time of a program is long, as the disk data must be loaded or an external module must be started before the program can provide services. In this case, you can use the container readiness check to determine whether the program has been started by checking the program process. If the container's readiness check fails, the cluster will block requests from accessing the container. If the container's readiness check succeeds, access to the container will be opened.

## Health Check Methods

<span id="TCPPortProbe"></span>

### TCP Port Probe

TCP port probe works as follows:
For a container that provides TCP communication services, the cluster periodically establishes a TCP connection with the container. If the connection is successful, the probe succeeds; otherwise, it fails. To select the TCP port probe method, you must specify the port that the container listens to.
For example, for a Redis container with a service port of 6379, if you configure TCP port probe for the container and specify the probe port to be 6379, then the cluster will periodically initiate a TCP connection to port 6379 of the container. If the connection is successful, the check succeeds; otherwise, it fails.

<span id="HTTPRequestProbe"></span>
### HTTP Request Probe

HTTP request probe is suitable for a container that provides HTTP/HTTPS services, where the cluster periodically initiates a HTTP/HTTPS GET request to the container. If the return code in the HTTP/HTTPS response is in the range of 200 - 399, the probe succeeds; otherwise, it fails. To use HTTP request probe, you must specify the port that the container listens to and the HTTP/HTTPS request path.
For example, for a container that provides HTTP services with a service port of 80 and HTTP check path of `/health-check`, the cluster will periodically initiate a `GET http://containerIP:80/health-check` request to the container.

### Run Command Check

Run command check is a powerful way of health check, which requires you to specify an executable command in a container that the cluster periodically runs. If the return result of the command is 0, the check succeeds; otherwise, it fails.
You can replace both [TCP port probe](#TCPPortProbe) and [HTTP request probe](#HTTPRequestProbe) by performing a run command check:

- For TCP port probe, you can write a program to connect to the container's port. If the connection succeeds, the script will return 0; otherwise, -1.
- For HTTP request probe, you can write a script to wget the container and check the return code of the response. For example, you can write `wget http://127.0.0.1:80/health-check`. If the return code is in the range of 200 - 399, the script will return 0; otherwise, -1.


> - The program to be run must be placed in the image of the container; otherwise, the run will fail as the program cannot be found.
> - If the command to be run is a shell script, you cannot directly specify the script as the run command; instead, you need to add the script's interpreter. For example, if the script is `/data/scripts/health_check.sh`, the specified program should be `sh /data/scripts/health_check.sh` when run command check is used.

## Other Common Parameters

- **Start delay**: In seconds. This specifies the time before the probe starts after the container is started. For example, if the start delay is set to 5, then the health check will start 5 seconds after the container is started.
- **Interval**: In seconds. This specifies the frequency of health checks. For example, if the interval is set to 10, then the cluster will be checked one every 10 seconds.
- **Response timeout**: In seconds. This specifies the timeout period for health probes. It indicates the TCP connection timeout period, the HTTP request response timeout period, and the run command timeout period for TCP port detection, HTTP request detection, and run command check, respectively.
- **Healthy threshold**: In times. It specifies the times of consecutive health check successes before it is determined that the container is healthy. For example, if the healthy threshold is set to 3, the container will be considered healthy only if 3 consecutive probes succeed.
 If the type of health check is a survival check, then the healthy threshold can only be 1, and other values you set will be considered invalid.
- **Unhealthy threshold**: In times. It specifies the times of consecutive health check failures before it is determined that the container is unhealthy. For example, if the unhealthy threshold is set to 3, the container will be considered unhealthy only if 3 consecutive probes fail.
