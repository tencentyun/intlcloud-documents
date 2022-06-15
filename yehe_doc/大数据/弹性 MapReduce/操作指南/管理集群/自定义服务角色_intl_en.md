The custom service role feature allows users to create a CAM service role for granting access to COS resources. Please select **Tencent Cloud Product Service** as the service type and **Elastic MapReduce** as the service supporting the role. If no custom service role is configured, the system uses the **EMRCosRole** role by default to access COS resources.

## Step 1. Customize a Permission Policy
Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), click **Create Custom Policy**, and select **Create by Policy Syntax** in the **Select Policy Creation Method** pop-up dialog box.
![](https://main.qcloudimg.com/raw/32521aa3647055cf2118e225a5edf56c.png)![](https://main.qcloudimg.com/raw/52d362b87d23e9c66acb18a1dfe53898.png)
On the **Create by Policy Syntax** page, select **Blank Template** as the template type.
![](https://main.qcloudimg.com/raw/8db8e6ca59519ea7aeea451974d494b5.png)
Set the syntax policy as follows:

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
Where `appId` is the AppID of the root account, and `bucketName` is the name of the bucket that you want to authorize. Generate a policy named `TestPolicy`. In practical cases, you can customize the name.

## Step 2. Create a Custom Role
In the [CAM console](https://console.cloud.tencent.com/cam/role), click **Create Role** to open the **Select role entity** dialog box, select **Tencent Cloud Product Service** to go to the **Create Custom Role** page, and select **Elasticsearch MapReduce (emr)** in **Services supporting roles**.
 ![](https://main.qcloudimg.com/raw/912520936e5ab438a0a29465df509c9a.png)
Bind the `TestPolicy` policy generated in step 1. In practical cases, You can bind a policy according to your business requirements.
![](https://main.qcloudimg.com/raw/e86f82c78c25462946822b3595e8fef9.png)
Generate a custom role named `EMRCosRole`. In practical cases, you can customize the name.
![](https://main.qcloudimg.com/raw/14ed1ae36b382cb48b3f54a1bea9d8fa.png)

## Step 3. Bind the Role with an EMR Cluster
In the [EMR console](https://console.cloud.tencent.com/emr), click a cluster ID to go to the instance information page and click **Set** next to **Custom Service Role** in the **Basic Configuration** section. Set the custom service role to the `EMRCosRole` role generated in step 2. In practical cases, you can customize the name.
![](https://main.qcloudimg.com/raw/af3721b9b7e6b4027c3df166ad16ec58.png)
