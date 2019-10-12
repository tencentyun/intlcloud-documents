## Scenario

When creating multiple instances, if you want the instance names to follow a particular pattern, you can choose to specify a pattern string or allow the system to automatically suffix the names with numbers in ascending order. You can do so on the purchase page or using TencentCloud APIs.

- If you need to purchase multiple instances and want to name them in the format of "CVM + number" (such as CVM1, CVM2, CVM3, etc.), you can do so by [configuring automatically suffixing instance names with numbers in ascending order](#AutoAscending).
- If you need to create multiple instances and you want the suffixes of the instance names starting from a certain number, you can do so by [specifying a single pattern string](#SpecifySingleString).
- If you need to create multiple instances and you want the instance names having multiple parts and the suffix of each part starting from a certain number, you can do so by [specifying multiple pattern strings](#SpecifyMultipleStrings).


## Directions

<span id="AutoAscending"></span>
### Configuring automatically suffixing instance names with numbers in ascending order

You can name the instances you buy in bulk with the same name body and suffix the names with numbers in ascending order.
> The instance names will be suffixed with numbers starting from 1 by default. You cannot specify the starting number.
>
For example, you want to buy three instances and name them in the format of "CVM + number" (i.e., CVM1, CVM2, and CVM3).

#### Configuring on the purchase page

1. Refer to [Create Instances](https://intl.cloud.tencent.com/document/product/213/4855) to purchase the instances. Fill `CVM` in “Instance Name” in the fourth step, "4. Security Group and CVM" as shown below:
![](https://main.qcloudimg.com/raw/9815074c0fde0f3dbc7f0b9f4504d7e3.png)
2. In the fifth step, "5. Confirm", enter the number of instances you want to buy (in this case, 3) in “Quantity”, click *Enable* to make the payment.
3. Go back to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to view the new instances. You will see that the instances are named with the same name body and are suffixed with numbers in ascending order as shown below:
![](https://main.qcloudimg.com/raw/34057be61529702cc287db4a971865d3.png)

### Configuring using API

In TencentCloud API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730), set the InstanceName field to `CVM`.

### Specifying pattern strings

By specifying pattern strings, you can name the instances you buy in bulk with complicated structures and suffix them with specified numbers. You can specify one or more pattern strings for instance names as needed.

If you specify pattern strings in the format of **{R:x}**, the instance names will be suffixed with numbers in ascending order starting from **x**.

<span id="SpecifySingleString"></span>
#### Specifying a single pattern string

For example, you need to create 3 instances and name the instances with ascending numbers starting from 3.

##### Configuring on the purchase page

1. Refer to [Create Instances](https://intl.cloud.tencent.com/document/product/213/4855) to purchase the instances, and fill **“name body + pattern string {R:x}”** (in this case, `CVM{R:3}`) in “Instance Name” in the fourth step, "4. Security Group and CVM" as shown below:
![](https://main.qcloudimg.com/raw/1b06d1bdf95e10afdd7dfde39e3a7e11.png)
2. In the fifth step, "5. Confirm", enter the number of instances you want to buy (in this case, 3) in “Quantity”, click *Enable* to make the payment.
3. Go back to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to view the new instances. You will see that the instances are named with the same name body and are suffixed with ascending numbers starting from 3 as shown below:
![](https://main.qcloudimg.com/raw/69d59d2523a9fc27a5b58d61070cfe21.png)

##### Configuring using API

In TencentCloud API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730), set the InstanceName field to `CVM{R:3}`.

<span id="SpecifyMultipleStrings"></span>
#### Specifying multiple pattern strings

For example, you want to create three instances and use instance names that contain three parts, **cvm**, **Big**, and **test**, with **cvm** and **Big** suffixed with ascending numbers starting from 13 and 2 respectively (i.e., cvm13-Big2-test, cvm14-Big3-test, and cvm15-Big4-test).

##### Configuring on the purchase page

1. Refer to [Create Instances](https://intl.cloud.tencent.com/document/product/213/4855) to purchase the instances, and fill **“part 1 + pattern string 1 {R:x}-part 2 + pattern string 2 {R:x}-part 3”** (in this case, `cvm{R:13}-Big{R:2}-test`) in “Instance Name” in the fourth step, "4. Security Group and CVM" as shown below:
![](https://main.qcloudimg.com/raw/6704d8309016c2406c51d3a3b99b6883.png)
2. In the fifth step, "5. Confirm", enter the number of instances you want to buy (in this case, 3) in “Quantity”, click *Enable* to make the payment.
3. Go back to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to view the new instances. You will see that the names of the instances contain all the three parts and the first two parts are suffixed with ascending numbers starting from 13 and 2 respectively as shown below:
![](https://main.qcloudimg.com/raw/2d6980c90ab552c911bdf16197c685f9.png)

#### Configuring using API

In TencentCloud API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730), set the InstanceName field to `cvm{R:13}-Big{R:2}-test`.
