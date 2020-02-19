## 1. Configuring scaling policy in advance
If you know when to scale out and scale in, you can set an Auto Scaling scheduling policy. At the corresponding time, the system will automatically add or remove a CVM instance, with no need for human efforts.

## 2. Coping with business volume surges with low costs

When the traffic arises, you need to prepare CVMs in advance to prevent CVM overload caused by the sudden surge in CPU utilization. When the traffic decrease, you need to reduce CVMs accordingly. With the Auto Scaling policy configured, the system will determine when to trigger scaling accordingly. When the monitoring metrics reach the threshold, then CVM instances are automatically added or removed, and Cloud Load Balancer configuration is automatically implemented. This reduces the cost for servers and also human efforts.

## 3. Replacing unhealthy CVMs automatically

To prevent your business from being affected by unhealthy CVMs, you need to constantly monitor the operation status of CVMs. With Auto Scaling, the system regularly performs health checks on CVMs. When the system detects an exceptional CVM instance, it automatically creates a new instance to replace the exceptional instance. You can check all the logs if necessary.
