## Overview

To allow you to name batch created CKafka instances according to a rule during creation, the features of automatically incrementing suffixed numbers and specifying pattern strings are provided.

- **Automatically incrementing suffixed numbers:** if you purchase multiple CKafka instances, numbers will be suffixed to their names by default, such as ckafka1, ckafka2, ckafka3... For more information, please see [Automatically incrementing suffixed numbers](#AutoAscending).

- **Specifying pattern string:**
  - **Specifying one pattern string:** this is suitable if you need to create n instances and specify their names with incrementing serial numbers starting from x (such as ckafka3, ckafka4, ckafka5...). For more information, please see [Specifying one pattern string](#SpecifySingleString).
  - **Specifying multiple pattern strings:** this is suitable if you need to create n instances named with multiple prefixes and specified serial numbers for each prefix (such as ckafka3-big10-test, ckafka4-big11-test, ckafka5-big12-test). For more information, please see [Specifying multiple pattern strings](#SpecifyMultipleStrings).

## Directions

### Automatically incrementing suffixed numbers[](id:AutoAscending)

This feature allows you to name batch purchased instances with the same prefix and automatically incrementing suffixed numbers.

>! 
>- The created instances are suffixed with numbers starting from 1 by default. You cannot specify the starting number.
>- The following example assumes that you want to purchase 3 CKafka instances and name them in the format of "ckafka+serial number" (i.e., ckafka1, ckafka2, and ckafka3).

<dx-tabs>
::: Operations\son\sthe\spurchase\spage
1. Purchase 3 instances as instructed in [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718). Enter the instance name in the format of **prefix+serial number**. In this case, enter `ckafka` as the instance name as shown below:
![](https://main.qcloudimg.com/raw/ddf73ac8cf503c93cd4ede057ded701e.png)
2. Follow the prompts on the page and make the payment.
:::

::: Operations\sthrough\sAPI
In the [ModifyInstanceAttributes](https://intl.cloud.tencent.com/document/api/597/35354) API, set the relevant fields:

Instance name: set `InstanceName` to `ckafka`.
:::
</dx-tabs>


### Specifying pattern string[](id:SpecifyStrings)

This feature allows you to name batch purchased instances in a complex format with specified serial numbers. You can use one or more pattern strings in instance names as needed.

The instance name with a specified pattern string is in the format of **{R:x}**, where `x` indicates the starting number in the generated instance names and can be positive integers only.


#### Specifying one pattern string[](id:SpecifySingleString)

The following example assumes that you want to create 3 instances and name them with incrementing numbers starting from 3.

<dx-tabs>
::: Operations\son\sthe\spurchase\spage
1. Purchase instances as instructed in [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718). Enter the instance name in the format of **prefix+specified pattern string {R:x}**. In this case, enter `ckafka{R:3}` as the instance name as shown below:
![](https://main.qcloudimg.com/raw/8fee4eadfcd092b41135de7d52a1595c.png)
2. Follow the prompts on the page and make the payment.
:::

::: Operations\sthrough\sAPI
In the [ModifyInstanceAttributes](https://intl.cloud.tencent.com/document/api/597/35354) API, set the relevant fields:

Instance name: set `InstanceName` to `ckafka{R:3}`.
:::
</dx-tabs>


#### Specifying multiple pattern strings[](id:SpecifyMultipleStrings)

The following example assumes that you want to create 3 instances and name them with the prefixes of `ckafka`, `big`, and `test` and serial numbers after `ckafka` and `big` incrementing from 13 and 2 respectively (i.e., ckafka13-big2-test, ckafka14-big3-test, and ckafka15-big4-test).

<dx-tabs>
::: Operations\son\sthe\spurchase\spage
1. Purchase 3 instances as instructed in [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718). Enter the instance name in the format of **"prefix+specified pattern string {R:x}-prefix+specified pattern string {R:x}-prefix"**. In this case, enter `ckafka{R:13}-big{R:2}-test` as the instance name as shown below:
![](https://main.qcloudimg.com/raw/7d064d5c4d374bbcb7284bf9100f3ab1.png)
2. Follow the prompts on the page and make the payment.
:::

::: Operations\sthrough\sAPI
In the [ModifyInstanceAttributes](https://intl.cloud.tencent.com/document/api/597/35354) API, set the relevant fields:

Instance name: set `InstanceName` to `ckafka{R:13}-big{R:2}-test`.
:::
</dx-tabs>


## Feature Verification

After you batch create instances through [automatically incrementing suffixed numbers](#AutoAscending) or [specifying pattern string](#SpecifyStrings), you can verify the set instance names as follows:

Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka) and view the newly created instances. You can see that the batch purchased instances are named according to the rule you set.

