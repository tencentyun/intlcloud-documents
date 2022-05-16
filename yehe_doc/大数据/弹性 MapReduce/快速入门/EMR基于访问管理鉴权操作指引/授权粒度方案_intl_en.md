## Six-Segment Resource Description
qcs: Describes the abbreviation of `qcloud service`. It indicates that the resource is a Tencent Cloud resource, which is required.
project_id: Describes the project information, which is used to enable compatibility with legacy CAM logic and can be left empty.
service_type: Describes the product abbreviation, such as `CVM`.
region: Describes the region information, such as `bj` (see the [CAM documentation](https://intl.cloud.tencent.com/document/product/598)).
account: Describes the root account of the resource owner, such as `uin/164256472`.
resource: Describes the detailed resource information of each product, such as `instance/instance_id1` or `instance/*`.

## Tag Authentication Operation Guide
This section describes how to authorize EMR tags. Before using tags to manage the authorization of EMR resources, you need to plan tags based on your departments or organizations; for example, you can plan usernames, clusters, and tags for departments A, B, and C respectively as shown below. For more information on tags, see [Tag](https://intl.cloud.tencent.com/document/product/651).
![](https://qcloudimg.tencent-cloud.cn/raw/4b5300d576143e5801e3d0ec7c68a52f.png)

After completing the planning, to enable department A to manage cluster A1, you need to perform the following operations in sequence.
### 1. Create a tag and tag the cluster
- Enter the [Tag List](https://console.cloud.tencent.com/tag/taglist) page and click **Create Tag**.
>? The `tag_A` tag is used as an example here and below.

![](https://qcloudimg.tencent-cloud.cn/raw/4d3ed40021f00d041d4ed6ac248784c0.png)

- Enter the tag key and tag value and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/4e7715aba63a8912a33078d2a6f42a1f.png)

- On the **[Cluster List]("qcs::emr:gz:uin/10000000001:emr-instance/*")** page, select the target cluster, click **More** at the top, and click **Edit Tag**.
![](https://qcloudimg.tencent-cloud.cn/raw/5860ed23838cad2372a3eb3b0174c7e3.png)

- On the **Edit Tag** page, select the created `tag_A` tag and click **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/ae56afde82a35b2942ae9c7079270858.png)

### 2. Create a custom policy

Currently, certain EMR APIs don't support authorization by tag; therefore, you need to set two policies: `Policy_Dept_A1` (for APIs that support authorization by tag) and `Policy_Dept_A2` (for APIs that don't).

- **Create custom policy `Policy_Dept_A1`**
    - Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console and click **Create Custom Policy**.
    - Select **Authorize by Tag**.
    - In **Tag Policy Generator**, select **Dept_A** for **Authorized Users**, leave **User Groups** empty, select the tag key and tag value of the planned tag for **Tag Key** and **Tag Value** respectively, and click **Next**.
    - Create the `Policy_Dept_A1` policy, replace the content of the `action` and `resource` fields with the following in **Policy**, and click **Complete**.   
    ```
                "action": [

                                    "emr:*"
                            ],
                            "resource": [
                                    "qcs::emr:gz:uin/10000000001:emr-instance/*"
                            ]
    ```

>! The content of the `resource` field needs to be entered based on the actual resource. For more information on value rules, see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).

- **Create custom policy `Policy_Dept_A2`**
    - Go to the **Policies** page in the CAM console and click **Create Custom Policy**.
    - Select **Create by Policy Syntax**.
    - In **Select Policy Template**, select **Blank Template** and click **Next**.
    - Create the `Policy_Dept_A2` policy, clear the existing content in **Policy**, paste the following content, and click **Complete**.
```
    {
            "version": "2.0",
            "statement": [
                    {
                            "effect": "allow",
                            "action": [
    "emr:RunJobFlow","emr:DescribeJobFlow","emr:FindClusterListForMC","emr:EmrScaleoutClusterWithAuth","emr:CreateClusterForMC","emr:CheckSoftRelation","emr:DescribeK8sResourcePrice","emr:DescribePodSpecs","emr:DescribePodSpec","emr:DescribeTkeWhiteList","emr:GenerateCreateGoodsDetail","emr:DescribeLogSearchFileNames","emr:DescribeEMRInstancesExtra","emr:DescribeClusterHardwareInfo","emr:DescribeInstanceServiceRoleNames","emr:DescribeServiceComponents","emr:DescribeCompareMetricsList","emr:DescribeHeatMapMetricList","emr:DescribeHBaseRegionList","emr:DescribeAutoScaleWhiteList","emr:DescribeOptionalSpecWhiteList","emr:DescribeServiceOverview","emr:DescribeEMRInstances","emr:DescribeEMRNodeType","emr:DescribeEMRNodes","emr:DescribeStepByTimeRange","emr:DescribeClusterOverview","emr:DescribeEMRNodeOverview","emr:DescribeNodeHardwareInfo","emr:DescribeTopNMeta","emr:DescribeMetricDataAutoGranularity","emr:DescribeLogSearchTabs","emr:DescribeEMRHostOverview","emr:DescribeLogSearchRecords","emr:DescribeTopNByProcess","emr:DescribeDiskInfo","emr:DescribeMetricInfo","emr:DescribeInstanceServiceAbstract","emr:ModifyMetricMetaPerInstance","emr:DescribeOverviewData","emr:DescribeClusterHardwareType","emr:DescribeClusterEmergencyCallback","emr:DescribeTopNByHost","emr:DescribeHeatMapDistribution","emr:DescribeInstanceServiceRoleTable","emr:DescribeEmrSaleInfoExtend","emr:DescribeNodeAlias","emr:DescribeInstanceNodes","emr:DescribeKeyPairs","emr:DescribeHbaseTableMetricData","emr:DescribeHbaseMetricMeta","emr:DescribeEmrMetaDB","emr:CheckMetaDBNet","emr:ModifyEmrRole","emr:DescribeEmrRole","emr:DescribeDisasterRecoverGroup","emr:DescribeTags","emr:InquiryPriceCreateInstance","emr:GetCreateGoodsDetail","emr:DescribleAccountBalance","emr:DescribeSecurityGroup","emr:DescribeMetricData","emr:DescribeEmrSaleInfo","emr:DescribeCvmSpec","emr:DescribeCdbPrice","emr:CreateInstance","emr:CheckCustomConfig","emr:CheckCosInfo","emr:GetCreateGoodsDetailList","emr:GetScaleoutGoodsDetailList","emr:GetRenewGoodsDetailList","emr:UpdateWebProxyPassForMcController","emr:SubmitServiceParamsForMC","emr:ReleaseClusterForMC","emr:RestartServiceForMC","emr:GetNodeListForMcController","emr:GetMetricDataForMcController","emr:GetServiceGroupForMcController","emr:EmrDestroyTaskNodeWithAuth",
    "emr:DescribeModifySpec","emr:DescribeMasterIp","emr:DescribeMetricsDimension"
                            ],
                            "resource": "*"
                    }
            ]
    }
```

### 3. Authorize and authenticate the sub-user
- On the **User List** page, find the target sub-user and click **Authorize** on the right. For more information on how to create a sub-user, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
- Select **Policy_Dept_A1** and **Policy_Dept_A2** and click **Complete**.
- Log in as a sub-user for authentication.
    At this point, when logging in to EMR, the sub-user can see and manage the `test_A` cluster only through the `tag_A` tag.
>! As the APIs in the `Policy_Dept_A2` policy can only be fully listed, a permission error may occur when new APIs are subsequently added. In case of such permission error, [submit a ticket](https://console.cloud.tencent.com/workorder/category) or [contact us](https://intl.cloud.tencent.com/contact-us) for assistance.

## Resource-Level and API-Level Authentication Operation Guide
This section describes how to authorize EMR resources. When using resource-level authentication to authorize an EMR feature, you need to plan resources for your departments or organizations first; for example, you can plan usernames, APIs, and clusters for departments A, B, and C as shown below.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f18ddcfe9b30d50b37b9c314e8e540bf.png" style="zoom:80%;" />
After completing the planning, to grant department A only access to the `DescribeRegionAndZoneSaleInfo` API of the cluster, you need to perform the following operations in sequence:

### 1. Create a custom policy

- Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console and click **Create Custom Policy**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8209bc089b8de53ce08c971f140e72a7.png" style="zoom:77%;" />
- Select **Create by Policy Syntax**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/88a47609cec96c049807c55b511fc034.png" style="zoom:80%;" />
- In **Select Policy Template**, select **Blank Template** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/f15d5c2461d2e5f0445bebc75b8dbb82.png)
- Create a custom policy named `DescribeRegionAndZoneSaleInfo-test`, clear the existing content in **Policy**, configure the access `deny` policy for EMR's `DescribeRegionAndZoneSaleInfo` API, and save the configuration.
```
    {
            "version": "2.0",
            "statement": [
                    {
                            "effect": "allow",
                            "action": [
    "emr: DescribeRegionAndZoneSaleInfo"
                            ],
                            "resource": "*"
                    }
            ]
    }
```

![](https://qcloudimg.tencent-cloud.cn/raw/ba20dc82456de18ef9768bc6265635ae.png)

>! For APIs that support resource-level authentication, see **List of APIs supporting resource-level authorization**. As the APIs can only be fully listed, a permission error may occur when new APIs are subsequently added. In case of such permission error, you can add the missing API permission in the policy according to the error message.

### 2. Authorize and authenticate the sub-account
- On the **User List** page, find the target sub-user and click **Authorize** on the right. For more information on how to create a sub-user, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
![](https://qcloudimg.tencent-cloud.cn/raw/d5ee8dc672ecdb6d71f4cd9ed2a103bb.png)
- Select the `DescribeRegionAndZoneSaleInfo-test` custom policy and click **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/2fa6240fb1a49108ec6878a9582feffa.png)
- After you log in with the sub-account and call the above API, if a pop-up window similar to the following requesting authorization is displayed, the authentication has been successfully configured.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fe904eba29bbf9541fdc9a0ca0cb0e38.png" style="zoom:80%;" />