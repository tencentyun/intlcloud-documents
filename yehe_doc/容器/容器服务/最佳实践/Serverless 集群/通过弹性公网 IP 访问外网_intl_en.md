
Currently, EKS allows you to bind an EIP to a Pod simply by declaring it in the template annotations. For more information, please see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

There are four annotations related to EIP:

| Annotation Key                                      | Annotation Value and Description                                      | Required                      |
| --------------------------------------------------- | ------------------------------------------------------------ | ----------------------------- |
| `eks.tke.cloud.tencent.com/eip-attributes`          | It indicates that the workload's Pod needs to be bound to an EIP. If the value is `""`, the binding will be created with the default EIP configuration. You can enter the EIP's TencentCloud API parameter JSON string in `""` to customize the configuration. | Yes if you want to bind an EIP |
| `eks.tke.cloud.tencent.com/eip-claim-delete-policy` | It indicates whether to repossess the EIP after the Pod is deleted. `Never` indicates not to repossess. The default value is to repossess.          | No                            |
| `eks.tke.cloud.tencent.com/eip-injection`           | If the value is `true`, the EIP's IP information will be exposed in the Pod, and you can run the `ip addr` command in the Pod to view the EIP address. | No                            |
| `eks.tke.cloud.tencent.com/eip-id-list`             | It indicates that an existing EIP will be used, and only StatefulSets are supported. After the Pod is terminated, its EIP will not be repossessed by default. Note that the number of StatefulSet Pods cannot exceed the number of `eipId` values specified in this annotation. | No                            |

1. If you want to bind an EIP to a workload or Pod for public network access, the simplest way is to add the `eks.tke.cloud.tencent.com/eip-attributes: ""` flag under the `annotation` of the corresponding workload or Pod as follows:
<dx-codeblock>
:::  yaml
metadata:
    name: tf-cnn
    annotations: 
    eks.tke.cloud.tencent.com/cpu: "8"
    eks.tke.cloud.tencent.com/gpu-count: "1"
    eks.tke.cloud.tencent.com/gpu-type: T4
    eks.tke.cloud.tencent.com/mem: 32Gi
    eks.tke.cloud.tencent.com/eip-attributes: ""  # An EIP is required and uses the default configuration
:::
</dx-codeblock>
2. Run the following command to view the relevant events:
```sh
kubectl describe pod [name]
```
You can see that there are two new events related to the EIP as shown below, which indicate a success.
![](https://main.qcloudimg.com/raw/41f3957b664b1dbfee1ade405d522560.png)
3. View the log file, and you can see that the datasets can be downloaded normally as shown below:
![](https://main.qcloudimg.com/raw/e0e02f6c1ec047bc09ead5f6259aad1f.png)
>!**The daily number of EIPs that can be applied for is limited**, so EIP is not suitable for tasks that need to run multiple times every day.
