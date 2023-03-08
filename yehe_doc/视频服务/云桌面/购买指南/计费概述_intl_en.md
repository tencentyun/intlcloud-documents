The hardware configuration of a CVD instance is determined by the [specification](#list) you choose when creating the instance. CVD offers a wide variety of specifications that come with different computing powers. You can choose computing power and storage space based on your service scale.

[](id:billing)
## Billing Modes

CVD instances differ in terms of compute resources (including vCPU and memory), management unit (standard or graphic), and storage resources (including system and data disks). You can determine the specifications of your desktops, the number of desktops you need, and the region based on your business scenario and the user base you serve. CVD offer two billing options, which are **prepaid monthly subscriptions** and **pay-as-you-go**.

| Billing Mode | Description                                                     | Use Case                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Monthly subscription | You need to pay for desktops in advance in order to use the services for a certain period of time, and you can determine whether you want to renew the subscription when it expires. | This mode is more cost-effective if you need virtual desktops for long-term use. |
| Pay-as-you-go | You request CVD resources on demand, and fees are charged based on your actual usage (with usage durations accurate down to the second). | This mode allows you to shut down desktops to release compute resources when they are not in use. It is more suitable for short-term uses. |

>?
>- Pay-as-you-go instances support "shut down to save cost". After you shut down a desktop, the system will reclaim the compute resources (vCPUs, memory, and GPUs) without terminating the desktop. Therefore, for shut down desktops, only storage fees (system disks and data disks) will be incurred. Compute resources will not be charged. This helps you reduce costs.
>- After an instance is shut down, its compute resources will be released. The instance may temporarily fail to start again. If this happens, try again or try later.
>- When you restart or reset a CVD instance, the instance may be automatically shut down. The "shut down to save cost" policy is not applicable in such cases.

## Desktop Specifications

* Compute resources: The compute resources of a CVD instance include CPUs, memory, and GPUs. You can choose different combinations based on your business needs.
* Management unit: A management unit provides support for end users' connection and use of a virtual desktop. CVD offers standard and graphic management units.
* Storage resources: A cloud disk stores the OS and user data. You can select an SSD or premium cloud disk.

CVD instances can be monthly subscribed or pay-as-you-go. For more information, see [Billing Modes](#billing).
>? When you return a monthly subscribed instance, fees are deducted from the refund amount based on how long you have used the desktop. For the portion of usage duration that spanned an entire month, the prices and discounts for monthly packages will apply; for additional usage, the pay-as-you-go rates will apply. For details, see [Refund](https://www.tencentcloud.com/document/product/1167/51915).

## Compute Resources

CVD offers compute resources in the form of packages. You can choose different specifications (CPUs, memory, GPUs) based on your business scenario.

| Specification | GPU | Recommended Scenarios | Monthly Subscription (USD/Month) | Pay-as-You-Go (USD/Hour) |
|---------|---------|---------|  -------- | --------------- |
| CVD - Standard S1_4-core 8 GB |  \ | Basic OA | 84.82 | 0.29 |
| CVD - Standard S1_4-core 16 GB | \ | OA | 145.39 | 0.37 |
| CVD - Standard S1_8-core 16 GB |  \ | High-performance OA and coding   | 206.61 |0.49|
| CVD - Graphic G1_4-core 16 GB |  1/4 NVIDIA T4 | Light 3D requirements, such as drawing viewer  | 296.88 | 0.8 |
| CVD - Graphic G1_8-core 32 GB |  1/2 NVIDIA T4 | Moderate 3D requirements, such as online design |498.57 | 1.22 |
| CVD - Graphic G1_16-core 64 GB |  1 NVIDIA T4 | Heavy 3D requirements, such as video editing | 901.93 |2.06 |

>? More CVD specifications will be available in the future.

## Management Unit

Management units come in two types – standard and graphic. When you buy a desktop instance, the system will automatically select a management unit according to the compute resources you purchase.

| Specification | Recommended Scenarios | Monthly Subscription (USD/Month) | Pay-as-You-Go (USD/Hour) |
| -------------------- | ------------ | ---------------------- | ------------------------ |
| CVD standard management unit | Standard OA | 3                      | 0.018                    |
| CVD graphic management unit | GPU OA  | 15                     | 0.12                     |

## Storage resources

Storage resources include system disks and data disks, each of which correspond to one cloud disk. You can select the disk type ([SSD](https://buy.cloud.tencent.com/cvd) or [Premium](https://buy.cloud.tencent.com/cvd)) and size as needed.

| CVD System Disk    | Monthly Subscription (USD/GB/Month) | Pay-as-You-Go (USD/GB/Hour) |
| ----------------- | ---------------  | --------------- |
| SSD cloud disk | 0.17 | 0.0003 |
| Premium cloud disk | 0.05 | 0.0001 |

| CVD Data Disk    | Monthly Subscription (USD/GB/Month) | Pay-as-You-Go (USD/GB/Hour) |
| ----------------- | ---------------  | --------------- |
| SSD cloud disk | 0.17 | 0.0003 |
| Premium cloud disk | 0.05 | 0.0001 |