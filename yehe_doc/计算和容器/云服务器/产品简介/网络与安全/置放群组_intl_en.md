A placement group is a policy for distributing instances on the underlying hardware. The instances you create in the placement group feature disaster recovery and high availability when launched. Tencent Cloud CVM provides an instance placement policy, which can force the instances to be dispersed with a certain policy and reduce the impact of the underlying hardware/software failure on CVM services. You can use the placement group to deploy CVM instances on different physical servers to ensure service high availability and the underlying disaster recovery capability. When you create instances in a placement group, we will launch them in a specified region according to the deployment policy you configured in advance. If you did not configure a placement group for the instances, we will try to launch them on different physical servers to ensure service availability.

## Spread Placement Group

Currently, spread placement group is supported. A spread placement group is a group of instances that are placed on different underlying hardwares and have high availability. We recommend that you use a spread placement group for applications of important instances that need to be placed separately, such as master/slave databases and high-availability clusters. By launching instances in a spread placement group, you can minimize the simultaneous failure of instances with the same underlying hardware.
A spread placement group is region specific and can be deployed across multiple availability zones. There is a limit on the number of instances that can be placed in a group. For more information, please see the [Console](https://console.cloud.tencent.com/cvm/ps).

> When you launch instances in a spread placement group, the request will fail if you have insufficient hardware. You can wait for a while and try again.

## Spread placement group rules and limits

Before using a spread placement group, note the following rules:
1. Placement groups cannot be merged.
2. An instance can only be added to one placement group.
3. Spread placement group can be placed on physical machines, switches, or racks.
4. The maximum number of instances supported by a spread placement group on a physical machine, switch, or rack is different. For more information, see the official website.
5. If you specify and use the disaster recovery group policy, it will be strictly followed. Please note that if there is not enough hardware to distribute instances, the creation of some instances will fail.
6. Dedicated CVM instances cannot be added to a spread placement group.

## Operation Guide
For more information on operations, see [Spread Placement Group](https://intl.cloud.tencent.com/document/product/213/17020).
