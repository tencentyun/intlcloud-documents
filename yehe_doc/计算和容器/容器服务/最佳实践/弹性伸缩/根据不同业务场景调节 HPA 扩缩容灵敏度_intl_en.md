## Overview

Before K8s v1.18, HPA scaling does not support adjusting sensitivity.

- For scale down, the scale down stabilization window is controlled by the `--horizontal-pod-autoscaler-downscale-stabilization-window` parameter of `kube-controller-manager`. The default value is 5 minutes, that is, it will take at least 5 minutes to scale down after the load is reduced.
- For scale up, the scale up velocity is controlled by fixed algorithm and hardcoding constant factor of HPA Controller, which cannot be customized.

The K8s design logic makes it impossible for users to customize the scaling sensitivity of HPA. But different applications have different requirements for scaling sensitivity, for example:

- Key applications that may have traffic spikes. They should scale up as fast as possible (to avoid traffic bottleneck), and scale down very slowly (waiting for another traffic spike).
- Offline applications that process a large amount of data. They should scale up as fast as possible during the peak hours to reduce the data processing time, and scale down as soon as possible after the peak hours to reduce the costs.
- Applications that process regular data/web traffic. They may scale up and down in a usual way to minimize jitter.

>? After the update of K8s 1.18 HPA, the scaling sensitivity is available for the previous v2beta2 version, and the version number remains unchanged as v2beta2.

This document provides scaling examples in the common use cases, and introduces how to use the new HPA feature of K8s 1.18 to control the scaling sensitivity, so as to better meet the requirements for scaling velocity in various scenarios.


## Examples

K8s 1.18 adds a new `behavior` field under HPA Spec, which provides two fields `scaleUp` and `scaleDown` to control the scale up and scale down behaviors respectively. 



### Scaling up as fast as possible

When you want to scale up quickly, you can create an HPA with the following configuration:

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
    name: web
spec:
    minReplicas: 1
    maxReplicas: 1000
    metrics:
    - pods:
        metric:
          name: k8s_pod_rate_cpu_core_used_limit
        target:
          averageValue: "80"
          type: AverageValue
      type: Pods
    scaleTargetRef:
      apiVersion: apps/v1
      kind: Deployment
      name: web
    behavior: # essential
      scaleUp:
        policies:
        - type: Percent
          value: 900
          periodSeconds: 15
```

The example indicates that 9 times the current number of pods can be added, effectively making the number of replicas 10 times the current size. The number of Pods cannot exceed the limit of `maxReplicas`.

For example, if the application is started with 1 pod, when it experiences traffic spikes, it will scale up as soon as possible with the following number of pods:

```
1 -> 10 -> 100 -> 1000
```

If the scale down policy is not configured, it will wait for the default scale down stabilization window (`--horizontal-pod-autoscaler-downscale-stabilization-window`, default value: 5 minutes), and then start scale down.




### Scaling up as fast as possible, scaling down very gradually

When an application experiences a sharp drops of the amount of concurrency after a traffic peak hour, the default scale down policy will be used, and the number of Pods will drop sharply after a few minutes. If the Pod experiences another traffic peak after the scale down, the application can still quickly scale up at this time. But the scale up process will take a certain time, and the traffic peak may last for a long time. During this time, the backend processing capacity of the application may reach a bottleneck, which may cause some request failures. You can configure the following `behavior` for HPA to gradually scale down after quickly scale up. Examples are as follows:

```yaml
behavior:
    scaleUp:
      policies:
      - type: percent
        value: 900%
    scaleDown:
      policies:
      - type: pods
        value: 1
        periodSeconds: 600 # Scale down 1 pod every 10 minutes
```

The `scaleDown` is configured in the example. It specifies that 1 Pod will be reduced every 10 minutes during scale down, which greatly reduces the scale down velocity. The number of Pods changed during scale down is as follows:

```
1000 -> … (10 min later) -> 999
```

With this configuration, the key applications can process scaling and avoid request failures during a peak traffic hour.




### Scaling up very gradually


For the non-critical applications that do not need quickly scale up, you can add the following `behavior` to HPA for gradual scale up. Examples are as follows:

```yaml
behavior:
    scaleUp:
      policies:
      - type: pods
        value: 1 # Add 1 Pod for each scale up
```

For example, if the application has 1 pod by default, it will scale up as follows:
```
1 -> 2 -> 3 -> 4
```

### Disabling automatic scale down

For the key applications that do not need automatic scale down after scale up, manual intervention or other self-developed controllers are required to determine the scaling conditions. You can configure the following `behavior` policy to disable automatic scaling. Examples are as follows:

```yaml
behavior:
    scaleDown:
      policies:
      - type: pods
        value: 0
```

### Extending scale down stabilization window

The default scale down stabilization window is 5 minutes (`--horizontal-pod-autoscaler-downscale-stabilization-window`). If you want to extend the stabilization window to avoid exceptions caused by some traffic glitches, you can specify the scale down stabilization window through the following `behavior` policy. Examples are as follows:

```yaml
behavior:
    scaleDown:
      stabilizationWindowSeconds: 600 # Wait 600 seconds (10 minutes) before starting scale down
      policies:
      - type: pods
        value: 5 # Scale down 5 pods each time
```

The example indicates that when the load is reduced, it will wait 600 seconds (10 minutes) before starting scale down, and only scale down 5 Pods each time.



### Extending scale up stabilization window




Some applications often frequently scale up due to data glitches. Actually Pods do not need scale up in a short period of time, and the scale up may cause waste of resources. For example, in the scenario of a data processing pipeline, the scale up metric is the number of events in the queue. When a large number of events heaps in the queue, scale up is performed only when the load continues to exceed the scale up threshold. If events heaps only for a short period of time, events can be processed quickly without scaling up the queue.

The default scale up algorithm will scale up in a short time. For the above scenarios, you can configure the following `behavior` policy to add a stabilization window for scale up to avoid resource waste caused by glitches. Examples are as follows:

``` yaml
behavior:
    scaleUp:
      stabilizationWindowSeconds: 300 # Stabilization window for waiting 5 minutes before scaling up
      policies:
      - type: pods
        value: 20 # Scale up 20 Pods each time
```

The example indicates that you need to wait for a stabilization window for 5 minutes before scaling up. If the load drops during this period, no scale up is performed. The scale up is performed only when the load continues to exceed the scale up threshold, and 20 Pods are added for each time.




## References

- [HPA Introduction](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
- [Configurable Scale Up/Down Velocity for HPA](https://github.com/kubernetes/enhancements/tree/master/keps/sig-autoscaling/853-configurable-hpa-scale-velocity)
