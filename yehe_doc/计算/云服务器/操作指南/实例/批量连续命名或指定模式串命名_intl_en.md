## Overview

To allow you to name batch created instances/hosts according to a rule during creation, the features of automatically incrementing suffixed numbers and specifying pattern strings are provided.

- When you need to purchase n instances and generate instance/host names in specific forms, such as "CVM+Sequence number" (for example, CVM 1, CVM 2, and CVM 3), you can use the feature of [Automatically Ascending Suffixed Numbers](#AutoAscending).
- When you need to create **n** instances and name specific instances/hosts with ascending numbers starting from **x**, you can use the feature of [Specifying a Single Pattern String](#SpecifySingleString).
- When you need to create n instances/hosts with multiple prefixes in their names, each of which contains a specified serial number, you can use the feature of [Specifying Multiple Pattern Strings](#SpecifyMultipleStrings).

## Application Scope

This document applies to **setting instance name** and **setting host name**.

## Directions

<dx-alert infotype="explain" title="">
This document uses setting instance name as an example. The procedure may vary slightly according to the name type.
</dx-alert>



### Automatically incrementing suffixed numbers[](id:AutoAscending)

This feature allows you to name batch purchased instances with the same prefix and automatically ascending suffixed numbers.
<dx-alert infotype="notice" title="">
The created instances are suffixed with numbers starting from 1 by default. You cannot specify the starting number.
</dx-alert>
The following example assumes that you have purchased three instances and want to name these instances in the form of "CVM+Sequence number" (for example, CVM 1, CVM 2, and CVM 3).

<dx-tabs>
::: Purchase page
1. Purchase three instances by referring to [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855). On the **Configure network and host** tab page, enter the instance name in the form of **Prefix+Sequence number**. In this case, enter `CVM` as the instance name.
![](https://main.qcloudimg.com/raw/820a52077080be5da4c1fb4715452e6b.png)
2. Follow the prompts on the page and complete payment.
:::
::: API
In the [RunInstances](https://intl.cloud.tencent.com/zh/document/product/213/33237) API, set the relevant fields:
- Instance name: set `InstanceName` to `CVM`.
- Host name: set `HostName` to `CVM`.
:::
</dx-tabs>


### Specifying pattern string[](id:SpecifyStrings)

This feature allows you to name batch purchased instances in a complex form with specified serial numbers. You can use one or more pattern strings in instance names as required.

The instance name with a specified pattern string is in the form of **{R:x}**, where **x** indicates the starting number in generated instance names.


#### Specifying one pattern string[](id:SpecifySingleString)

The following example assumes that you want to create three instances and name them with ascending numbers starting from 3.

<dx-tabs>
::: Purchase page
1. Purchase three instances by referring to [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855). On the **Configure network and host** tab page, enter the instance name in the form of **Prefix+Specified pattern string {R:x}**. In this case, enter `CVM{R:3}` as the instance name.
![](https://main.qcloudimg.com/raw/4e09732d612222f619cf7a1e8da1ee06.png)
2. Follow the prompts on the page and complete payment.
:::
::: API
In the [RunInstances](https://intl.cloud.tencent.com/zh/document/product/213/33237) API, set the relevant fields:
- Instance name: set `InstanceName` to `CVM{R:3}`.
- Host name: set `HostName` to `CVM{R:3}`.
:::
</dx-tabs>


#### Specifying multiple pattern strings[](id:SpecifyMultipleStrings)

The following example assumes that you want to create three instances and name them with the **cvm**, **Big**, and **test** prefixes, where **cvm** and **Big** are followed by ascending numbers starting from 13 and 2, respectively. For example, their names are cvm13-Big2-test, cvm14-Big3-test, and cvm15-Big4-test, respectively.

<dx-tabs>
::: Purchase page
1. Purchase three instances by referring to [Creating Instances via CVM Purchase Page](http://intl.cloud.tencent.com/document/product/213/4855). On the **Configure network and host** tab page, enter the instance name in the form of **Prefix+Specified pattern string {R:x}-Prefix+Specified pattern string {R:x}-Prefix**. In this case, enter `cvm{R:13}-Big{R:2}-test` as the instance name.
![](https://main.qcloudimg.com/raw/1042e86262bc7ce3939f1842a8025c23.png)
2. Follow the prompts on the page and complete payment.

:::
::: API
In the [RunInstances](https://intl.cloud.tencent.com/zh/document/product/213/33237) API, set the relevant fields:
- Instance name: set `InstanceName` to `cvm{R:13}-Big{R:2}-test`.
- Host name: set `HostName` to `cvm{R:13}-Big{R:2}-test`.
:::
</dx-tabs>


## Feature Verification
After you batch create instances through [automatically incrementing suffixed numbers](#AutoAscending) or [specifying pattern string](#SpecifyStrings), you can verify the feature as follows:

### Verifying instance name
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and view the newly created instances. You can see that the batch purchased instances are named according to the rule you set as shown below:
![](https://main.qcloudimg.com/raw/a3c5e58daf07381ffde5abc019edad33.png)

### Verifying host name
1. [](id:hostname_step01)Restart and log in to the CVM instance.
2. Select different steps according to the instance's operating system:
<dx-tabs>
::: Linux instance
On the operating system UI, run the following commands:
```
hostname
```
:::
::: Windows instance
Open the command line tool and run the following command:
```
hostname
```
:::
</dx-tabs>
3. [](id:hostname_step03)View the returned result of the `hostname` command.
If the returned result is similar to the following, the setting is successful.
```
cvm13-Big2-test
```
4. Repeat [step 1](#hostname_step01)–[step 3](#hostname_step03) to verify other batch purchased instances.



