
## Pricing
>? Native node is a TKE cloud product billed separately. Its pricing is different from that of that of the Cloud Virtual Machine (CVM) service. The billing information of different specifications of native nodes is subject to that displayed on the console.
>


TKE native nodes support multiple types of CVM instances. You can select appropriate instances to deploy based on your application scale and business characteristics. TKE charges resources (including CPU, memory, GPU, and system disk resources) consumed by native node instances according to the instance type and resource specifications.

**Billing formula: Fees** = **Unit price of the native node instance resource configuration** * **Running time**

|    Billing Item      | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Instance type | Instance types supported by the current native node are as follows: (For more information, see [CVM instances](https://intl.cloud.tencent.com/document/product/213/11518))<li>Standard: S2, S5, SA2, SA3<li>Computing: C3, C4<li>Memory optimized: MA3, M5<li>GPU: GN7, GNV4, PNV4<li>High I/O: IT5 |
| Resource specifications | Resource specifications supported by the current native node are as follows: (Subject to those displayed on the console)<li>CPU: Two cores or more<li>Memory: 2 GB or more<li>System disk: Premium Cloud Storage or SSD, 50-1024 GB<li>GPU: Only GPU native node instances contain GPU resources and support only entire GPUs. |

## Billing Modes
TKE provides only one billing mode for native node instances: pay-as-you-go. Details are as follows:

| **Billing Mode**     | **Pay-as-you-go**                                   |
| -------- | ---------------------------------------------- |
| Payment method | Postpaid (Fees are frozen upon purchase and settled hourly)      |
| Billing unit | USD/second |
| Unit price | High |
| Minimum usage duration | Billed by second and settled by hour. You can purchase or release resources at any time. |
| Use cases | Suitable for periodic computing scenarios such as transcoding, big data, and e-commerce flash sale campaigns, or tidal online service scenarios where Horizontal Pod Autoscaler (HPA) is enabled. |

### Pay-as-you-go  
**Billing formula: Fees = Number of requested native node instances × Unit price of the native node instance resource configuration (by usage) × Usage duration**
When you activate a pay-as-you-go native node instance, the fees (including CPU, memory, GPU, and system disk fees) for 1-hour usage based on the resource configuration unit price will be frozen in your account balance as a deposit. You will then be billed by the hour (Beijing time) for your usage over the past hour. When you purchase a native node instance, the unit price will be listed as an hourly fee. However, you will actually be billed by the second and the fees will be rounded to the nearest two decimal places. Billing starts from the second the native node instance is purchased and stops the second the instance is terminated. When the instance is terminated, the frozen amount will be unfrozen.

## References
- [Overdue Payment](https://www.tencentcloud.com/document/product/457/53360)
