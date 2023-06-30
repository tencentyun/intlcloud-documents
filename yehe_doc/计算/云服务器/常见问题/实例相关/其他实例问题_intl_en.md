
[](id:Q1)
### How do I view the operation logs of a CVM?
You can view the operation logs of a CVM on the console as follows:
1. Log in to the [CVM console](https://console.intl.cloud.tencent.com/cvm/instance/index?rid=4) and select **Tool** > **Operation Log** in the top-right corner.
2. Select **CVM** for the resource event and configure other filters as needed.
3. Click **Query** to obtain the CVM operation logs.
For more information about CloudAudit operation records, see [Viewing the Event Details of Operation Records](https://intl.cloud.tencent.com/document/product/1021/40499).


[](id:Q2)
### What if I cannot find my CVM in the console?
The reasons why a purchased CVM instance cannot be found in the CVM console include:
1. The instance is not located in the current region.
2. You did not log in to the right console.
3. No resource is available under the current account.
4. The instance is released due to overdue payment or expiration.
5. The spot instance is automatically repossessed.
6. Refund is caused by insufficient resources.

For detailed solutions, see [A CVM Instance Cannot Be Found](https://www.tencentcloud.com/document/product/213/51460).


[](id:Q3)
### How to view the CPU frequency of a CVM?
The frequency viewed via `/proc/cpuinfo` on a Linux instance is only the base frequency, because some privileged registers on the virtual machine cannot be accessed and the underlying real-time running frequency information of the CPU cannot be read. For information on CPU models and frequencies of instances, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).


[](id:Q4)
### How to enable turbo frequency for a CVM?
Turbo frequency is enabled automatically when a CVM is running. The processor will automatically adjust the running frequency based on the CPU loading requirements of the application. The max turbo frequency can be reached when a CPU intensive application is running.







