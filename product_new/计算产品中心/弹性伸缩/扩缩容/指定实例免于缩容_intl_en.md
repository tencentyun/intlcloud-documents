## Introduction
Removal Protection allows you to ensure a CVM will not be removed in scale-in.

You can enable **Removal Protection** for one or more instances in a scaling group. You can modify the scaling group or the instance protection configuration at any time.

If scaling activity occurs when all the remaining instances in the scaling group are marked with “Removal Protection”, AS will decrease the desired capacity instead of removing any instances.

## Scenario

Normally, the CVMs in a scaling group are stateless, and can be removed at any time. However in the following circumstances, you may need to prevent the instances from being removed in scale-in:

- **One CVM for multiple uses:** If the CVM in the cluster is also used for other purposes, for example, it is also used for storing the data generated in the cluster, so this CVM is actually stateful.

- **Avoid misoperation:** If you worry that the business will be affected due to a policy setup error, you can set a **Removal Protection** for some CVMs. In this way, AS will never remove these CVMs in scale-in, and the tunnel "Request-LB-CVM" will remain unblocked.

## Setting Up
In the list of the CVMs of the scaling group, you can configure this directly:
![](https://mc.qcloudimg.com/static/img/f913547df4ed60c7aecb8784b1965a07/1.jpg)
