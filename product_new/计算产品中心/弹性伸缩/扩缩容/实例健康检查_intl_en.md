If you specify the **Initial Capacity** when creating a new scaling group, after the launch configuration and scaling group have been created, the scaling group will create the same number of CVM instances as the initial number of instances. Meanwhile, the scaling group will ensure that the number of running instances is larger than the **Min Capacity** and smaller than the **Max Capacity**.
>!
> - Min Capacity: The minimum number of instances allowed in the auto scaling group. When the number of instances in the group is smaller than this value, scale-out is triggered and AS adds instances, making the number of instances equal to the mini capacity.
> - Initial Capacity: The initial number of CVMs when the scaling group is created.
> - Max Capacity: The maximum number of instances that is allowed in a scaling group. When the number of instances in the group is larger than this value, scale-in is triggered and AS removes instances, making the number of instances equal to the maximum scaling group size.

To ensure the normal operations of the instances in the scaling group, AS periodically performs health checks on the instances. If it is found that the running status of a CVM instance is unhealthy, AS will stop this CVM and launch a new CVM.

- **Instance health check**

The scaling group periodically checks the running status of instances to confirm whether each instance is robust (whether it responses to the ping command within 1 minute). If the pinged instance is unreachable for more than one minute, AS marks this instance as unhealthy.

- **Replacing unhealthy instances**

If an instance is marked as unhealthy, the scaling group will immediately replace it with a newly launched instance, unless it is under "Removal Protection".
