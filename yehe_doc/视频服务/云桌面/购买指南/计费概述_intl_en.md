When you create a CVD instance, the [specification](#list) you specify determines its server hardware configuration. CVD offers a wide variety of specifications, each of which provides different computing powers. You can flexibly choose the instance computing power and storage space based on the service scale to be sustained.

[](id:billing)
## Billing Modes

CVD specifications include compute resources (vCPU and memory) and storage resources (system disk and data disk). You can determine the specification, quantity, and geographical distribution of CVD instances to be purchased based on where your end users are located and your business scenarios, so as to deliver the optimal CVD service. CVD supports two billing modes: **monthly subscription (prepaid)** and **pay-as-you-go (postpaid)**.


| Billing Mode 	| Payment Mode 	| Use Case |
|---------|---------|---------|
| Monthly subscription | [](id:annually) Prepaid mode. You need to pay the fees when creating a CVD instance and then select whether to renew it based on the usage. | Suitable for businesses with long-term stable CVD needs as it is cheaper than pay-as-you-go billing. |
| Pay-as-you-go | [](id:paid) Postpaid mode. You can request for CVD resources on demand and will be charged based on the actual usage upon settlement (with the usage duration accurate down to the second). | Suitable for businesses with short-term CVD needs. Instances can be shut down as needed to release compute resources to save costs. |

>?
>* Pay-as-you-go CVD instances support the "shut down to save cost" feature; that is, if your instance is shut down and retained, the system will automatically repossess compute resources (vCPU, memory, and GPU) and charge fees only for storage resources (system and data disks) but not compute resources.
>* After an instance is shut down, its compute resources will be released. The instance may temporarily fail to start again. If this happens, try again or try later.
>* When you restart or reset a CVD instance, the instance may need to be automatically shut down and restarted, during which the "shut down to save cost" policy will not be executed.

[](id:list)
### CVD instance specifications

* Compute resources: The compute resources of a CVD instance include different combinations of CPU and memory specifications, which you can select flexibly based on your business needs.
* Storage resources: You can select an SSD or premium cloud disk of the desired size as the system or data disk of the CVD instance to sustain OS or user data resources.

CVD instances can be monthly subscribed or pay-as-you-go. For more information, see [Billing Modes](#billing).
>?As of the day when the CVD instance is refunded, if the usage has lasted for one month or longer, fees will be calculated at the corresponding monthly subscription price and discount listed on the official website; otherwise, fees will be calculated at the pay-as-you-go price. For more information, see [Refund](https://www.tencentcloud.com/document/product/1167/51915).

## Compute Resources
The compute resources of CVD instances are offered in the form of packages. The compute power varies by the instance specification determined by the combinations of CPU, memory, and GPU for different business scenarios.

| Specification | GPU | Recommended Scenarios | Monthly Subscription (USD/Month) | Pay-as-You-Go (USD/Hour) |
|---------|---------|---------|  -------- | --------------- |
| CVD - Standard S1_4-core 8 GB |  \ | Basic OA | 77.75 | 1.49 |
| CVD - Standard S1_4-core 16 GB | \ | OA | 133.27 | 1.83 |
| CVD - Standard S1_8-core 16 GB |  \ | High-performance OA and coding   | 170.92 |3.33|
| CVD - Graphic G1_4-core 16 GB |  1/4 NVIDIA T4 | Light 3D requirements, such as drawing viewer  | 296.88 | 3.83 |
| CVD - Graphic G1_8-core 32 GB |  1/2 NVIDIA T4 | Moderate 3D requirements, such as online design |498.57 | 5.97 |
| CVD - Graphic G1_16-core 64 GB |  1 NVIDIA T4 | Heavy 3D requirements, such as video editing | 901.93 |10.28 |
>?More CVD specifications will be available in the future.

## Storage Resources
The storage of an instance is divided into system disk and data disk, each of which are sustained by a cloud disk. You can choose [SSD cloud disk](https://buy.cloud.tencent.com/cvd) or [premium cloud disk](https://buy.cloud.tencent.com/cvd) and customize the disk size as needed.

| CVD System Disk    | Monthly Subscription (USD/GB/Month) | Pay-as-You-Go (USD/GB/Hour) |
| ----------------- | ---------------  | --------------- |
| SSD cloud disk | 1 | 0.0025 |
| Premium cloud disk | 0.35 | 0.0009 |

| CVD Data Disk    | Monthly Subscription (USD/GB/Month) | Pay-as-You-Go (USD/GB/Hour) |
| ----------------- | ---------------  | --------------- |
| SSD cloud disk | 1 | 0.0025 |
| Premium cloud disk | 0.35 | 0.0009 |
