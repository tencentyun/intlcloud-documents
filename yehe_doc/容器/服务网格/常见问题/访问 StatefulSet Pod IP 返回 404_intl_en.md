404 is returned when a service container in Istio accesses a pod IP address in the same cluster, but the access in istio-proxy is normal.

## Cause

A StatefulSet pod uses headless SVC. In Istio, the support for headless SVC is not the same as that for ordinary SVC. If the pod uses ordinary SVC, the corresponding listener has a passthrough route, that is, the packet will be forwarded to the real destination IP+Port corresponding to the packet. The headless SVC has no such processing. Because the headless SVC does not have a vip, its route is determined, that is, the route points only to the fixed pods in the backend. If the route cannot be matched, a problem occurs. If passthrough routing is also used on the headless SVC, the problem is just masked. Therefore, no passthrough route is created for the headless SVC. For the same service, this problem occurs only when the service is migrated to Istio. It can be considered as a design or implementation issue of Istio.

## Sample Scenario

The service uses its own service discovery and therefore directly uses a pod IP address to call the StatefulSet's pod IP address.

## Solution

When accessing the StatefulSet's pod IP address in the same cluster, include the host in the request to match the headless SVC's route, thereby avoiding 404 due to a matching failure.

