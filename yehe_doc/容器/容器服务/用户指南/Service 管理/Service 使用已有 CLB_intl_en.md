

Tencent Kubernetes Engine (TKE) allows you to use the `service.kubernetes.io/tke-existed-lbid: <LoadBalanceId>` annotation to specify CLB instances associated with cluster services. It also provides the **CLB reuse by services** feature that allows you to specify multiple services to use the same existing CLB.

## Synchronization Behavior for Using Existing CLBs
* When an existing CLB is used, the annotation that specifies the service network type does not take effect.
* When a service stops using an existing CLB, the listener of the service will be deleted and the CLB will be retained.
When the listener is deleted, the system checks whether the listener name was modified. If the listener name was modified, the listener may have been created by a user and will not be proactively deleted.
* If a service is using an automatically created CLB, the annotation for using an existing CLB added for the service will cause the current CLB to end its lifecycle and be released. The service configuration is synchronized to the existing CLB. If the annotation for using an existing CLB is deleted for the service, `Service Controller` will create a CLB for the service and synchronize the service configuration to the created CLB.

## Notes
- The specified CLB must be in the same region as the cluster.
- Your TKE containers and CVMs cannot share a CLB.
- You cannot operate CLB listeners and backend servers managed by TKE in the CLB console. Your updates will be overwritten by TKE automatic synchronization.
- When an existing CLB is used:
  - `Service Controller` is not responsible for the release or reclamation of the existing CLB.
  - Only CLBs created in the CLB console can be reused. CLBs automatically created by TKE cannot be reused. If these CLBs are reused, the CLB lifecycle management of other services will be affected.
- When **CLBs are reused**:
  - CLBs cannot be reused across clusters.
  - We recommend implementing clear management of listener ports. Otherwise, the management of CLBs reused by multiple services may be disordered.
  - When a CLB to be reused has a port conflict, CLB reuse is prohibited. If a conflict occurs during modification, backend synchronization for the listener with the conflict may be incorrect.
  - Local access cannot be enabled for services that reuse the same CLB (a limitation of traditional CLBs).
  - When you delete a service that reuses a CLB with other services, the backend server bound to the reused CLB needs to be unbound manually. The `tke-clusterId: cls-xxxx` tag retained for the CLB also needs to be manually cleared.


## Service Example
```Yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
  name: nginx-service
spec:
  ports:
    - name: 80-80-no
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```
>
>- The `service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx` annotation indicates that the service uses an existing CLB for configuration.
>- The service type must be set to `LoadBalancer`.


## Use Case
### Exposing TCP and UDP services over the same port
Kubernetes has a limitation on its service design, which requires that multiple port protocols exposed under the same service must be the same. In many game scenarios, users must expose TCP and UDP services over the same port. The CLB service provided by Tencent Cloud can monitor UDP and TCP simultaneously over the same port. To meet users' requirements for exposing TCP and UDP services over the same port, you can have services reuse a CLB.
For example, in the following service configuration, `game-service` is described as two services. Except for the listening protocol, the content of these two services is basically the same. You can annotate the two services to use the existing CLB `lb-6swtxxxx` and use kubectl to apply these two services to the cluster. In this way, multiple protocols can be exposed over the same CLB port.
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
  name: game-service-a
spec:
  ports:
    - name: 80-80-tcp
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: game
  type: LoadBalancer
------------------------------------------------
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
  name: game-service-b
spec:
  ports:
    - name: 80-80-udp
      port: 80
      protocol: UDP
      targetPort: 80
  selector:
    app: game
  type: LoadBalancer
```
