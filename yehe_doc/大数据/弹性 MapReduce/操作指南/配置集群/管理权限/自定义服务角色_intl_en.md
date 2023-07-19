The custom service role feature enables you to create a CAM service role for granting access to COS resources. Please select **Tencent Cloud Product Service** as the service type and **Elastic MapReduce** as the service supporting the role. If no custom service role is configured, the system uses the **EMRCosRole** role by default to access COS resources. 

## Step 1. Customize a Permission Policy
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), click **Create Custom Policy**, and select **Create by Policy Syntax** in the **Select Policy Creation Method** pop-up window.
2. On the **Create by Policy Syntax** page, select **Blank Template** as the template type.
3. Set the syntax policy as follows:
```
{
		"version": "2.0",
		"statement": [
			{
					"action": "cos:*",
					"effect": "allow",
					"resource": "qcs::cos::uid/appId:bucketName/*"
			}
		]
}
```
Where `appId` is the AppID of the root account, and `bucketName` is the name of the target bucket. Generate a policy named `TestPolicy`. In practical cases, you can customize the name.

## Step 2. Create a Custom Role
1. In the [CAM console](https://console.cloud.tencent.com/cam/role), click **Create Role** to open the **Select role entity** pop-up window, select **Tencent Cloud Product Service** to go to the **Create Custom Role** page, and select **Elasticsearch MapReduce (emr)** in **Product Service**.
2. Associate the `TestPolicy` policy generated in step 1. In practical cases, you can associate a policy as needed.
3. Set the role tag keys and values and click **Next**.
4. Generate a custom role named `EMRCosRole`. In practical cases, you can customize the name.

## Step 3. Bind the Role with an EMR Cluster
In the [EMR console](https://console.cloud.tencent.com/emr), click a cluster ID/name to go to the instance information page, select **Instance info** > **Basic configuration** > **Custom Service Role** and then click **Set**. Set the custom service role to the `EMRCosRole` role generated in step 2. In practical cases, you can customize the name.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cnrw860_%E5%9B%BD%E9%99%8580.png)
