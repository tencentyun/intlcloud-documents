## Introduction
Anti-DDoS Pro supports custom advanced DDoS protection policies. You can customize protection policies according to your service features or the nature of attacks. In general, you can associate at most one advanced DDoS protection policy with an Anti-DDoS Pro instance. If you have multiple instances, you can set up to 5 advanced DDoS protection policies.
You may need to continuously optimize the policies to keep up with actual business needs and ever-changing attacks. To streamline the management of refined DDoS protection, Anti-DDoS Pro allows you to create scenarios. You can create scenarios, and the backend can collect, identify, and automatically generate advanced protection policies for flexible configuration or maintenance of policies.
## Creating a Scenario
- **Method 1:**
If you have not configured any scenario for your Anti-DDoS Pro instance yet, when you log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Protection Configuration** in the left sidebar, you will see a message as shown below. Click **Create Now** to create a scenario.
![](https://main.qcloudimg.com/raw/6464fbb25cbabca6e0e05551ef024a7e.png)
>You can create up to 5 scenarios.
- **Method 2:**


1. Log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Protection Configuration** in the left sidebar. Select the **Advanced DDoS Protection Policy** tab and click **Create Scenario**.
![](https://main.qcloudimg.com/raw/fc9a5f67e5e9bbd7486342f0e3eab7da.png)
1. In the **Create Scenario** box, configure the following parameters according to your service features and click **OK** to complete the configuration.
	- **Scenario Name:** required; enter a scenario name with a length of 1-32 characters.
	- **Platform:** select the development platform of your service. The options include PC client, mobile, TV, and host.
	- **Category:** select a service category. The options include game, application, website, and others.
	- **Basic Information:**
		- **Current Protocol:** Select the protocol currently in use. The options include ICMP, TCP, UDP, and others.
>If you select TCP or UDP, you will need to enter the TCP/UDP service port range. You will also see an item in the **Other Information** area where you can configure the length of TCP/UDP service packet (optional; the length range is 0-1500 by default).
		- **Users Outside China**
Select **Yes** or **No**, indicating disabling or enabling **Block traffic from outside China**.
		- **Initiate outbound TCP requests**
Select **Yes** or **No**. If you select **Yes**, you need to enter the ports that initiate outbound TCP requests. Use commas (,) to separate multiple ports.
		- **Initiate outbound UDP requests, e.g., DNS, NTP requests, etc.**
Select **Yes** or **No**. If you select **Yes**, you need to enter the ports that initiate outbound UDP requests. Use commas (,) to separate multiple ports.

	- **Other Information**: click **Expand** to configure more parameters.
	- **Does the UDP payload have a fixed attribute?**
	Select **Yes** or **No**. **No** is selected by default. If you select **Yes**, you need to enter the UDP payload attributes.
	- **Does the TCP payload have a fixed attribute?**
	Select **Yes** or **No**. **No** is selected by default. If you select **Yes**, you need to enter the TCP payload attributes.
	- **Is there any web API service?**
	Select **Yes** or **No**. **No** is selected by default. If you selected **Yes**, you need to enter the API service URL(s). Use commas (,) to separate multiple URLs.

 ![](https://main.qcloudimg.com/raw/a5527197d8d8480f06f0d5f6bb3db064.png)
1. The backend will analyze the scenario you create and will automatically generate an advanced protection policy named in the format of “scenario name_policy_Number”, e.g., “test_policy_1”. You can then configure or modify the protection policy as needed.
>- If you only have one Anti-DDoS Pro instance and have created only one scenario, the generated advanced protection policy will be automatically associated with the instance.
	- If you modify the scenario information, the related configuration items in the corresponding advanced protection policy will be automatically modified to keep up with the changes to the scenario. However, changes to the advanced policy will not be synchronized to the corresponding scenario.

## Modifying and Deleting a Scenario
1. Log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Protection Configuration** in the left sidebar.
1. In the **Advanced DDoS Protection Policy** tab, click **Configure** or **Delete** to the right of the target scenario to modify or delete the scenario.
>If a scenario is deleted, the advanced protection policy corresponding to the scenario will also be deleted.
>
![](https://main.qcloudimg.com/raw/65f745bad99b8bdea356d428bc1466ce.png)
For more information, please see [Managing Advanced DDoS Protection Policies](https://intl.cloud.tencent.com/document/product/1029/31762).
