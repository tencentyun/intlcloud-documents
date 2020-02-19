1. **Creating HAVIPs**
Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/havip), and create an HAVIP. For more information on the operations, see [Creating HAVIPs](https://cloud.tencent.com/document/product/215/20129).
2. **Binding and configuration**
The configuration is the same as that in the traditional mode. The backend server declares and negotiates on the device that will be bound with the created HAVIP. You simply need to specify the virtual IP address in the configuration file as HAVIP.
In the cluster manager, add the HAVIP that was just created.
 ![1](https://main.qcloudimg.com/raw/960af4c34f05cf71432c0143176db3c2.png)
3. **Verification**
After the configuration is completed, directly switch nodes for testing.
 ![2](https://main.qcloudimg.com/raw/528373c391c718451acab0db9594ec04.png)
In normal situations, you will see that the network recovers after a short interruption (no interruption will be noticed at all if the switching is fast enough), and online services will not be affected.
 ![3](https://main.qcloudimg.com/raw/de5e3fd284d55c38c0a134efc1badf23.png)
 
