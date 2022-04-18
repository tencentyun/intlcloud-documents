### Back-off restarting failed docker container

Description: An exceptional Docker container is being restarted.
Solution: Check if the Docker process running in the image has exited due to an exception. If there is no process running in the image, you can add an execution script in the service creation page.

### fit failure on node: Insufficient cpu

Description: The cluster CPU is insufficient.
Solution: The node cannot provide enough computing cores. Modify the CPU limit on the service page or scale out the cluster.

### no nodes available to schedule pods

Description: Cluster resources are insufficient.
Solution: The reason for this error is that the number of nodes is not sufficient to carry the Pods. From the service page, modify the number of service Pods, the number of Pods or the CPU limit.

### pod failed to fit in any node

Description: There is no proper node for the Pod to use.
Solution: This error is caused when the service configures an inappropriate resource limit, which leads to a situation where there are no proper nodes to carry the Pods. Modify the number of service Pods or the CPU limit from the service page.

### Liveness probe failed

Description: The container health check failed
Solution: Check if the container processes in the image are normal, and whether the health check port is correctly configured.

### Error syncing pod, skipping 

Error syncing pod, skipping failed to "StartContainer" for with CrashLoopBackOff: "Back-off 5m0s restarting failed container
Description: The container process crashed or exited.
Solution: Check whether there is a foreground process that is persistently running. If so, check whether it is exceptional. For more information, see [Building a Docker Image Guide](https://intl.cloud.tencent.com/document/product/457/9115).

[Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) if the solutions offered above failed to resolve your issues.
