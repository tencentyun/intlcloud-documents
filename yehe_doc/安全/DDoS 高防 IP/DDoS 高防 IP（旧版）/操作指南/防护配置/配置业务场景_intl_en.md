## Use Cases
Anti-DDoS Advanced supports custom advanced DDoS protection policies. You can customize protection policies according to your business characteristics or the nature of attacks. In general, you can associate at most one advanced DDoS protection policy with an Anti-DDoS Advanced instance. If you have multiple instances, you can configure up to 5 advanced DDoS protection policies.
You may need to continuously optimize the policies to keep up with actual business needs and ever-changing attacks. To streamline the management of refined DDoS protection, Anti-DDoS Advanced allows you to create scenarios. You can create scenarios, and the backend can collect, identify, and automatically generate advanced protection policies for flexible configuration or maintenance of policies.
## Creating Scenario
- **Method 1:**
If you have not configured any scenario for your Anti-DDoS Advanced instance yet, when you log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar, you will see a message as shown below. Click **Create Now** to create a scenario.

>You can create up to 5 scenarios.
- **Method 2:**


1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar. Select the **Advanced DDoS Protection Policy** tab and click **Create Scenario**.

1. On the scenario creation page, configure the following parameters according to your business characteristics and click **OK** to complete the configuration.

	- **Scenario Name:** required; enter a scenario name containing 1–32 characters of any type.
	- **Platform:** select the development platform of your business. The options include PC client, mobile, TV, and CVM.
	- **Category:** select a service category. The options include game, application, website, and others.
	- **Basic Information:**
		- **Users outside China**
		Select **Yes**, **No**, or **Unknown**, indicating disabling or enabling **Reject traffic from outside China**.
		- **Actively initiate outbound TCP requests**
Select **Yes**, **No**, or **Unknown**. If you select **Yes**, you need to enter the ports that initiate outbound TCP requests. Use commas (,) to separate multiple ports.
		- **Actively initiate outbound UDP requests, such as DNS, NTP requests**
Select **Yes**, **No** or **Unknown**. If you select **Yes**, you need to enter the ports that initiate outbound UDP requests. Use commas (,) to separate multiple ports.
	- **Other Info**: click **Expand** to configure more parameters.
		- **UDP payload with fixed characteristic**
Select **Yes** or **No**. **No** is selected by default. If you select **Yes**, you need to enter the UDP payload characteristic.
		- **TCP payload with fixed characteristic**
Select **Yes** or **No**. **No** is selected by default. If you select **Yes**, you need to enter the TCP payload characteristic.
		- **Web API application (separated with comma ",")**
Select **Yes** or **No**. **No** is selected by default. If you selected **Yes**, you need to enter the API service URL(s). Use commas (,) to separate multiple URLs.
1. The backend will analyze the scenario you created and then automatically generate an advanced protection policy named in the format of `scenario name_policy_number`, such as `test_policy_1`. You can then configure or modify the protection policy as needed.
>
> - If you **have only one Anti-DDoS Advanced instance (resource)** and **have created only one scenario**, **the generated advanced protection policy will be automatically associated with the instance (resource)**.
- **If you modify the scenario information, the related configuration items in the corresponding advanced protection policy will be automatically modified to keep up with the changes to the scenario.** However, changes to the advanced policy will not be synchronized to the corresponding scenario.
>  - When one or more instances (resources) are bound to an advanced protection policy named "scenario name_policy_number.", if the forwarding rule parameters (such as the following parameters) of one instance (resource) are modified, **the corresponding configuration item information in the advanced protection policy will be automatically synced**.
>  - (Layer-4) Non-website business: TCP/UDP protocols; forwarding port range.
>  - (Layer-7) Website business: HTTP/HTTPS protocols; the forwarding ports are 80/443 by default.


## Modifying and Deleting Scenario
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar.
2. Click **Advanced DDoS Protection Policy** and click **Configure** or **Delete** on the right of the target scenario to modify or delete the scenario.
>If a scenario is deleted, the advanced protection policy corresponding to the scenario will also be deleted.

For more information, please see [Managing Advanced DDoS Protection Policy](https://intl.cloud.tencent.com/document/product/297/34217).
