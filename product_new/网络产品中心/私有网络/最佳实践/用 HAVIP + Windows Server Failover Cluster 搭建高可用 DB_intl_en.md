1. **Creating HAVIPs**
Log in to the [VPC console](https://console.cloud.tencent.com/vpc/havip) and create a HAVIP. For detailed directions, see [Creating HAVIPs](https://intl.cloud.tencent.com/document/product/215/31820#.E5.88.9B.E5.BB.BA-havip).
2. **Binding and configuration**
The configuration is the same as that in the traditional mode. The backend server declares and negotiates on the device that will be bound with the created HAVIP. You simply need to specify the virtual IP address in the configuration file as HAVIP.
In the cluster manager, add the HAVIP that was just created.
3. **Verification**
After the configuration is completed, directly switch nodes for testing.
In normal situations, you will see that the network recovers after a short interruption (no interruption will be noticed at all if the switching is fast enough), and online services will not be affected.

