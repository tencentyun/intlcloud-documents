Two trigger creation methods are provided for HTTP-triggered functions: default creation and custom creation, which have different billing logic.

### Default Creation
If you select "default creation", SCF will automatically create a basic API Gateway trigger, which provides only an access URL invisible in the console. In this case, an HTTP-triggered function is billed as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/4678ec7ab597d2e9e99e425066d84c8a.png)

- **Trigger side**: invocation is not billed, and outbound traffic is billed on the function side.
- **Function side:** in addition to standard billable items, the outbound traffic is also billed. 

>! A basic API Gateway instance will be created in default creation mode. You can upgrade it to the standard edition in the SCF console. After upgrade, you can use all gateway capabilities, which will be billed in the standard API Gateway billing method. The upgrade is irreversible.

### Custom creation
If you select "custom creation", you need to select a trigger type in the SCF console and bind a created service. In this case, the current billing method applies, where the function and trigger are billed according to their own billing rules respectively. Taking a standard API Gateway trigger as an example, an HTTP-triggered function is billed as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/62fedfe9cfb7bc483141a5990229d08d.png)
- **Trigger side:** the trigger is billed according to the billing rules of the product itself.
- **Function side:** the function is billed by standard billable items (invocations, resource usage, and outbound traffic), and the response traffic isn't billed on the function side.

### Trigger Capability Comparison
|| Default Creation (Basic API Gateway) | Custom Creation (Standard API Gateway) |
|------|--------|--------|
| Default domain name | Supported | Supported |
| Binding to custom domain name | Manual binding | Management in API Gateway console |
| Request method configuration | Supported | Supported |
| Release environment configuration | Supported | Supported |
| Authentication method configuration | Supported | Supported |
| Visibility in API Gateway console | Invisible | Visible |
| Advanced API Gateway capabilities (such as plugin and dedicated instance) | Not supported | Supported |
| Billing method | Gateway calls are not billed. | It is billed by standard API Gateway billable items. |
| Type conversion | The gateway can be upgraded to a standard API Gateway instance. After upgrade, you can use all gateway capabilities and billed by standard API Gateway billable items. | The gateway edition cannot be changed. A standard API Gateway instance cannot be rolled back to a basic API Gateway instance in default creation. |
