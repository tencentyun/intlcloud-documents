## Introduction
If you have purchased different Tencent Cloud resources, you can use tags to group the resources for easy management. You can grant different sub-accounts management permissions by tags so that they can manage resources separately. This document takes a use case as an example to describe how to grant a sub-account the permission to manage separate Tencent Cloud resources by using tags.

## Prerequisites
Suppose that:
 > - The enterprise account `CompanyExample` has two sub-accounts `DevA` and `DevB`.
 > - The ID of sub-account `DevA` is `12345`.
 > - The ID of sub-account `DevB` is `67890`.
 > - The enterprise account `CompanyExample` has two CVM instances whose IDs are `ins-1` and `ins-2` respectively.
 > - The enterprise account `CompanyExample` has two tag keys (`test1` and `test2`) and two tag values (`test1` and `test2`).

## Directions
<span id="biaoji"></span>
### Tagging CVM instances
You can add tag keys and tag values to CVM instances `ins-1` and `ins-2` with the following steps to manage resources by tag.
#### Adding `test1` tag key and `test1` tag value to CVM instance `ins-1`

1. Log in to the [Tag Console](https://console.cloud.tencent.com/tag), set the following filters to filter out the target CVM instance, and click **Query Resource**.
 - Resource Type: type of the resource to be queried. Only products supporting tags can be queried. For more information, please see [Products That Support Tags](https://intl.cloud.tencent.com/document/product/651/32577). In this example, select CVM instance.
 - Region: region of the resource to be queried. In this example, select Beijing.
2. Select the target CVM instance from the filtered results. In this example, we select CVM instance `ins-1`.
3. Click **Edit Tag Value**.
4. In the pop-up window, select the tag key and enter the tag value. In this example, the tag key and value are both `test1`.
5. Click **OK** to add `test1` tag key and `test1` tag value to CVM instance `ins-1`.

#### Adding `test2` tag key and `test2` tag value to CVM instance `ins-2`
1. Log in to the [Tag Console](https://console.cloud.tencent.com/tag), set the following filters to filter out the target CVM instance, and click **Query Resource**.
 - Resource Type: type of the resource to be queried. Only products supporting tags can be queried. For more information, please see [Products That Support Tags](https://intl.cloud.tencent.com/document/product/651/32577). In this example, we select CVM instance.
 - Region: region of the resource to be queried. In this example, we select Beijing.
2. Select the target CVM instance from the filtered results. In this example, we select CVM instance `ins-2`.
3. Click **Edit Tag Value**.
4. In the pop-up window, select the tag key and enter the tag value. In this example, the tag key and value are both `test2`.
5. Click **OK** to add `test2` tag key and `test2` tag value to CVM instance `ins-2`.

### Authorizing user by tag
You can grant sub-account `DevA` management permission for tag key `test1` and tag value `test1` and grant sub-account `DevB` tmanagement permission for tag key `test2` and tag value `test2`. They will then be able to manage tagged resources accordingly.
#### Granting sub-account `DevA` management permission for tag key `test1` and tag value `test1`
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) and click **Create Custom Policy** in the top-left corner.
2. In the creation method selection window that pops up, click **Authorize by Tag** to enter the authorization by tag page.
3. Select the following information and click **Next**.
 - Authorize User/User Group: check the user/user group to be authorized. In this example, `12345` is selected, which is the ID of sub-account `DevA`.
 - Tag Key: select the tag key to be authorized. In this example, we select tag key `test1`.
 - Tag Value: select the tag value to be authorized. In this example, we select tag value `test1`.
 - Resources: the management permission is granted by default.
4. On the verification page, enter the policy name, verify the policy content, and click **Done** to grant sub-account `DevA` management permission for tag key `test1` and tag value `test1`.

#### Granting sub-account `DevB` management permission for tag key `test2` and tag value `test2`
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) and click **Create Custom Policy** in the top-left corner.
2. In the creation method selection window that pops up, click **Authorize by Tag** to enter the authorization by tag page.
3. Select the following information and click **Next**.
 - Authorize User/User Group: check the user/user group to be authorized. In this example, `67890` is selected, which is the ID of sub-account `DevB`.
 - Tag Key: select the tag key to be authorized. In this example, we select tag key `test2`.
 - Tag Value: select the tag value to be authorized. In this example, we select tag value `test2`.
 - Resources: the management permission is granted by default.
4. On the verification page, enter the policy name, verify the policy content, and click **Done** to grant sub-account `DevB` management permission for tag key `test2` and tag value `test2`.

### Managing new resources

Follow the instructions in [Tagging CVM Instances](#biaoji) to add tag keys and tag values to manage new resources.
