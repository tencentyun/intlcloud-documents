

Tencent Kubernetes Engine (TKE) supports existing Cloud Load Balancers (CLBs) by using the `service.kubernetes.io/tke-existed-lbid: <LoadBalanceId>` annotation. You can use this annotation to specify a CLB instance to be associated with cluster service resources. TKE also provides the feature of **CLB sharing by multiple services**, which allows you to specify multiple services to share an existing CLB. To configure this feature, refer to the sample configuration in this document.

## Synchronization for Using Existing CLBs
* When an existing CLB is used, the network-type annotation of the specified service does not work.
* When a service no longer uses an existing CLB, the listener corresponding to the service will be deleted, but the CLB will be retained.
When a listener is deleted, the name of the listener is checked to verify whether it has been modified by the user. If yes, the listener is considered as created by the user and therefore cannot be automatically deleted.
* If a service is using an automatically created CLB, adding the annotation for using an existing CLB to this service terminates the lifecycle of the current CLB, which will be released accordingly. The configuration of the service will be synchronized with the CLB. Likewise, if the annotation for using an existing CLB is deleted from a service, the Service Controller component will create a CLB for the service and perform synchronization.


## Tencent Cloud Tag Synchronization for Using Existing CLBs
- By default, the tag `tke-createdBy-flag = yes` is configured for all CLBs created by services. When a service is terminated, the corresponding resources are deleted. If an existing CLB is used, this tag is not configured, and the corresponding resources are not deleted when the service is terminated.
- The tag `tke-clusterId = ` is configured for all services. If the ClusterId is correct, the tag is deleted when the service is terminated.
- For clusters created after August 17, 2020, the feature of sharing the same CLB among multiple services is disabled by default. For the changes and details of CLB tag configuration rules created by services in clusters before and after the aforementioned date, see [Multiple Services Sharing a CLB](https://intl.cloud.tencent.com/document/product/457/38336).




## Notes:
- The specified CLB must be in the same VPC as the cluster.
- Ensure that your TKE service and CVM service do not share the same CLB.
- You cannot use the CLB console to manage the listeners and servers bound to the TKE-managed CLBs. Your modification will be overwritten during automatic synchronization by TKE.
- When existing CLBs are used:
  - The Service Controller is not responsible for the release and repossession of the existing CLBs.
  - Only CLBs created in the CLB console can be used. CLBs automatically created by TKE cannot be shared because this affects the CLB lifecycle management of other services.
- When CLBs are **shared**:
  - A CLB cannot be shared across clusters.
  - When you need to use this **sharing** feature, we recommend that you implement robust listener port management. Otherwise, chaos may occur when a CLB is shared by multiple services.
  - In case of port conflict, CLB sharing is disabled. If a conflict occurs during modification, synchronization may be improper at the listener backend.
  - For services that share a CLB, local access is disabled (restriction for Classic CLBs).
  - When you delete a service that shares an existing CLB, you must manually unbind the real server that is bound to the CLB. The tag `tke-clusterId: cls-xxxx` is retained for the CLB, and can only be cleared manually.


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
>?
>- `service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx` indicates that the service uses an existing CLB for configuration.
>- Note that the service type must be set to `LoadBalancer`.


## Use Cases
### Using a monthly subscription CLB to provide services to external users
When the Service Controller component manages CLB lifecycles, it only supports the purchase of pay-as-you-go CLBs. When you need to use a CLB for a long term, the monthly subscription mode is more cost-effective. In such cases, you can purchase and manage CLBs independently, use annotations to control the use of existing CLBs by services, and remove CLB lifecycle management from the Service Controller component.

### Opening the TCP and UDP services in the same port
According to the official Kubernetes restrictions in service design, when multiple port protocols are opened under the same service, these protocols must be the same. In many game scenarios, users need to simultaneously open the TCP and UDP services in the same port. Tencent CLBs support simultaneous listening on UDP and TCP over the same port. This demand can be met through CLB sharing by multiple services.
For example, in the following service configuration, `game-service` is described as two service resources. The descriptions are basically the same except for the protocols for listening. Both services specify the use of an existing CLB `lb-6swtxxxx` through annotations. By applying the resources to a cluster through kubectl, multiple protocols can be exposed over the same CLB port.
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
