
## Problems 
The Pod suddenly kept restarting, with abnormal traffic coming in.

## Cause 
1. The Pod drifted to another node for start, as its previous node was abnormal.
2. After recreation, the Pod started slowly due to a faulty dependent service of the basic image. As both `ReadinessProbe` and `LivenessProbe` were configured, it was highly likely that all health checks failed more times than the upper limit set in `LivenessProbe`, thereby leading to a restart.
3. The Pod was configured with `preStop` for graceful termination, indicating to run `preStop` before restart. The graceful termination took a long time, and during `preStop` execution, `ReadinessProbe` kept probing.
4. TCP probe was used. During graceful termination, the TCP probe succeeded (port listening existed before the process was completely closed), but the process no longer processed new requests.
5. The result of `ReadinessProbe` but not `LivenessProbe` determines whether a Pod is ready. As `ReadinessProbe` was successful during `preStop` execution, the Pod became ready.
6. The Pod was ready but couldn't process requests, leading to business exceptions.

## Summary 
1. The Pod kept restarting due to a slow start and liveness probe. You need to prolong `initialDelaySeconds` or [StartProbe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes) to protect containers that start slowly.
2. The TCP probe method cannot reflect the actual health status of the business. During graceful termination, `ReadinessProbe` succeeds and lets traffic in, which will not be handled by the business, leading to traffic exceptions. We recommend you use a better probe method, where the business provides the HTTP liveness probe to check the actual health status of the business.
 
