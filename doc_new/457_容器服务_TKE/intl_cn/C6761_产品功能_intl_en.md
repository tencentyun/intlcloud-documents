## Cluster Management
TKE allows you to manage your container clusters easily and efficiently while ensuring security and reliability, enabling seamless integration with Tencent Cloud's computing, storage, and networking capabilities.

| Module | Feature |
|---|------|
| Cluster Composition | <li>Creates and adds exiting CVM instances of all models as nodes to clusters</b><br> <li>Supports cross-AZ deployment of nodes in a cluster</b><br> <li>Supports pay-as-you-go billing</b><br><li>User-exclusive clusters; isolates clusters through VPCs </b><br><li>Customizes cluster network and configures container network as you need |
| Cluster Management | <li>Supports cluster scaling, node scale-in/out </b><br> <li>Provides rich monitoring metrics; supports custom alarm policies</b><br> |
| Kubernetes Management | <li>Supports multiple Kubernetes editions and edition upgrage</b><br><li>Manages Kubernetes certificates; manipulates clusters directly using kubectl </b><br> <li>Easily manages namespaces in the console |

## Application Management
The application management feature of TKE can help you quickly create multiple services and deploy applications in different operating environments.

| Module | Feature |
|---|------|
| Application Composition | <li>Supports various types of TKE services </b><br> <li>Supports Kubernetes Deployment, DaemonSet  and other resource types|
| Application Management | <li>Creates applications quickly using "My Templates" or templates in the Template Market </b><br> <li>Supports real-time comparison of updated applications</b><br> <li>Deploys and stops services in an application with one click |
| Template Management | <li>Supports "My Templates" and Template Market</b><br> <li>Duplicates templates in one click|

## Service Management
Service management provides an efficient container management solution including various features such as quick creation of service, quick scaling, load balancing, service discovery, service monitoring, and health check, making it easier for you to manage your containers.

| Module | Feature |
|---|------|
| Service Deployment | <li>Supports service deployment in single-pod multi-container manner </b><br> <li>Supports multiple service access methods</b><br> <li> Supports cross-AZ deployment of pods in a service </b><br> <li>Configures affinity and anti-affinity scheduling |
| Service Management | <li>Supports rolling updates and fast updates of services</b><br> <li>Supports dynamical scaling of services </b><br> <li>Supports remote login for containers in services |
| Service OPS | <li>Checks detailed monitoring data of services in different metrics</b><br> <li>Checks `stdout` and `stderr` logs of containers in services</b><br> <li>Configures alarm policies for services </b><br> <li>Configures health check (survival check and readiness check) </b><br> <li>Auto-recovers containers in case of exception |

## ConfigMap Management
ConfigMaps are used to specify the read-in settings of some programs when they are started. You can use different ConfigMaps for different objects.

| Module | Feature |
|---|------|
| ConfigMap Management | <li>Multiple ConfigMap versions are supported </b><br> <li>Two editing forms are supported, i.e., visualization and YAML |
| ConfigMap Use | <li>Mounts ConfigMaps to container directory as volumes </b><br> <li>Imports ConfigMaps as environment variables </b><br> <li>Uses ConfigMaps in place of application template variables |

## Image Management
Tencent Cloud Image Registry contains official Docker Hub images and private images. Image management enables you to quickly create images and deploy services.

| Module | Feature |
|---|------|
| Image Management | <li>Creates private image repositories</b><br> <li>Checks and uses DockerHub image repositories</b><br> <li>Checks and uses TencentHub image repositories</b> <br> <li>Manages multiple image namespaces|
| Image Use | <li>Creates images through hi-speed private network</b><br><li>Uploads and downloads images over a public network |
| CI/CD | <li>Auto-building of private images can be set </b><br> <li>Image triggers can be set</b><br>|
