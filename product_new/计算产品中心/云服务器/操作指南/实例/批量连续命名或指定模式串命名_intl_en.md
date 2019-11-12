## Scenario

To allow you to name batch created CVM instances according to a rule during creation, the features of automatically ascending suffixed numbers and specifying pattern strings are provided.

- When you need to purchase n instances and generate instance names in specific forms, such as “CVM+Sequence number” (for example, CVM 1, CVM 2, and CVM 3), you can use the feature of [Automatically Ascending Suffixed Numbers](#AutoAscending).
- When you need to create **n** instances and name specific instances with ascending numbers starting from **x**, you can use the feature of [Specifying a Single Pattern String](#SpecifySingleString).
- When you need to create n instances with multiple prefixes in their names, each of which contains a specified serial number, you can use the feature of [Specifying Multiple Pattern Strings](#SpecifyMultipleStrings).


## Steps

<span id="AutoAscending"></span>
### Automatically Ascending Suffixed Numbers

This feature allows you to name batch purchased instances with the same prefix and automatically ascending suffixed numbers.
>Created instances are suffixed with numbers starting from 1 by default. The starting suffix number is fixed.
>
The following example assumes that you have purchased three instances and want to name these instances in the form of “CVM+Sequence number” (for example, CVM 1, CVM 2, and CVM 3).

#### Operations on the Purchase Page

1. Purchase three instances by referring to [Create an Instance](http://intl.cloud.tencent.com/document/product/213/4855). On the **2. Security Group and CVM** tab page, enter the instance name in the form of **Prefix+Sequence number**. In this case, enter `CVM` as the instance name.
![](https://main.qcloudimg.com/raw/9815074c0fde0f3dbc7f0b9f4504d7e3.png)
2. Follow the prompts on the page and complete payment.
3. Return to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to view the newly purchased instances. You can see that these batch purchased instances are named with the same prefix and ascending suffixed numbers.
![](https://main.qcloudimg.com/raw/34057be61529702cc287db4a971865d3.png)

#### API Operations

In the [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730) API, set the InstanceName field to `CVM`.

### Specifying Pattern Strings

This feature allows you to name batch purchased instances in a complex form with specified serial numbers. You can use one or more pattern strings in instance names as required.

The instance name with a specified pattern string is in the form of **{R:x}**, where **x** indicates the starting number in generated instance names.

<span id="SpecifySingleString"></span>
#### Specifying a Single Pattern String

The following example assumes that you want to create three instances and name them with ascending numbers starting from 3.

##### Operations on the Purchase Page

1. Purchase three instances by referring to [Create an Instance](http://intl.cloud.tencent.com/document/product/213/4855). On the **2. Set the CVM** tab page, enter the instance name in the form of **Prefix+Specified pattern string {R:x}**. In this case, enter `CVM{R:3}` as the instance name.
![](https://main.qcloudimg.com/raw/1b06d1bdf95e10afdd7dfde39e3a7e11.png)
2. Follow the prompts on the page and complete payment.
3. Return to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to view the newly purchased instances. You can see that these batch purchased instances are named with the same prefix and ascending suffixed numbers starting from 3.
![](https://main.qcloudimg.com/raw/69d59d2523a9fc27a5b58d61070cfe21.png)

##### API Operations

In the [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730) API, set the InstanceName field to `CVM{R:3}`.

<span id="SpecifyMultipleStrings"></span>
#### Specifying Multiple Pattern Strings

The following example assumes that you want to create three instances and name them with the **cvm**, **Big**, and **test** prefixes, where **cvm** and **Big** are followed by ascending numbers starting from 13 and 2, respectively. For example, their names are cvm13-Big2-test, cvm14-Big3-test, and cvm15-Big4-test, respectively.

##### Operations on the Purchase Page

1. Purchase three instances by referring to [Create an Instance](http://intl.cloud.tencent.com/document/product/213/4855). On the **2. Set the CVM** tab page, enter the instance name in the form of **Prefix+Specified pattern string {R:x}-Prefix+Specified pattern string {R:x}-Prefix**. In this case, enter `cvm{R:13}-Big{R:2}-test` as the instance name.
![](https://main.qcloudimg.com/raw/6704d8309016c2406c51d3a3b99b6883.png)
2. Follow the prompts on the page and complete payment.
3. Return to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to view the newly purchased instances. You can see that these batch purchased instances are named with prefixes followed by ascending numbers starting from the specified numbers.
![](https://main.qcloudimg.com/raw/2d6980c90ab552c911bdf16197c685f9.png)

##### API Operations

In the [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730) API, set the InstanceName field to `cvm{R:13}-Big{R:2}-test`.

