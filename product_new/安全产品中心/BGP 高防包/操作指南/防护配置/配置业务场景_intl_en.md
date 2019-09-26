## Application Scenarios
Anti-DDoS Pro supports custom DDoS advanced protection policies. You can set a policy according to your business features or the nature of the attacks. In general, you can bind at most one DDoS advanced protection policy to an Anti-DDoS Pro instance. If multiple instances exist in your account, you can select from up to 5 DDoS advanced protection policies.
You may need to continuously optimize the policy configuration to keep up with actual business needs and the ever-changing nature of attacks. To simplify DDoS refined protection management, Anti-DDoS Pro supports scenario settings. You can create scenarios, collect, identify, and automatically generate advanced protection policies. This allows for flexible configuration or maintenance policies.
## Creating a Scenario
- **Method 1:**
If you have not configured any scenarios for your Anti-DDoS Pro instance, log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Protection Configuration** in t he left sidebar. The prompting message shown in the following figure will appear. Click **Create Now** to create a scenario.
![](https://main.qcloudimg.com/raw/6d48443f59cbe498ef2f1387adfcbe69.png)
>You can create up to 5 scenarios.
- **Method 2:**


1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Protection Configuration** in the left sidebar. On the displayed page, choose **DDoS Advanced Protection Policy** -> **Create Scenario**.
![](https://main.qcloudimg.com/raw/881942d97b75abebdae9ae6a3d1b883a.png)
1. On the **Create Scenario** page, set the following parameters according to the actual business features and click **OK**. Then the service is configured.
	- **Scenario Name:** Mandatory. Enter a scenario name with 1-32 characters.
	- **Platform:** Select the development platform of your service. The options include PC, mobile, TV, and host.
	- **Category:** Select a service category. The options include game, application, website, and others.
	- **Basic Information:**
		- **Protocol in Use:** Select a protocol in use. The options include ICMP, TCP, UDP, and others.
>If you select TCP or UDP, you need to enter the TCP/UDP service port range. At the same time, the configuration window (optional) of TCP/UDP service packet length range will appear in the **Other Information** area. By default, the range is 0-1500.
		- **Users outside China**
Select **Yes** or **No**, indicating disabling/enabling **Block traffic from outside China**.
		- **Initiate outbound TCP requests**
Select **Yes** or **No**. If you select **Yes**, you need to enter the outbound port. Use commas (,) to separate multiple request service ports.
		- **Initiate outbound UDP requests (for example, DNS, NTP, and other requests)**
Select **Yes** or **No**. If you select **Yes**, you need to enter the outbound port. Use commas (,) to separate multiple request business ports.

	- **Other Information**: (Click **Expand** to select the corresponding parameters.)
	- **Fixed UDP payload attributes**
	Select **Yes** or **No**. **No** is selected by default. If you select **Yes**, you need to enter the UDP payload attributes.
	- **Fixed TCP payload attributes**
	Select **Yes** or **No**. **No** is selected by default. If you select **Yes**, you need to enter the TCP load features.
	- **Web API service**
	Select **Yes** or **No**. **No** is selected by default. If you selected **Yes**, you need to enter the API service URL. Use commas (,) to separate multiple URLs.

 ![](https://main.qcloudimg.com/raw/e97a9e85475d7a851403c8017e21fb26.png)
1. The backend analyzes the created scenarios and automatically generates an advanced protection policy in the “scenario name_policy_No.” format, for example, “test_policy_1”. You can then configure by yourself or adjust the protection policy as required.
>- If you only have one Anti-DDoS Pro instance and have created only one scenario, the generated advanced protection policy will be automatically bound to the instance.
	- If you have modified the scenario information, the generated advanced protection policy will automatically synchronize the related configuration item information. However, modification of this advanced policy will not be synchronized to the corresponding scenario.

## Modifying and Deleting a Scenario
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Protection Configuration** in the left sidebar.
1. On the **DDoS Advanced Protection Policy** page, find the target scenario and click **Configure** or **Delete** to modify or delete the scenario.
>The corresponding advanced protection policy will also be deleted together with the deletion operation.
>
![](https://main.qcloudimg.com/raw/e9df4c3e5d1ee9e668e685d263d2605e.png)
For more information, please see [Managing DDoS Advanced Protection Policy](https://intl.cloud.tencent.com/document/product/1029/31762).
