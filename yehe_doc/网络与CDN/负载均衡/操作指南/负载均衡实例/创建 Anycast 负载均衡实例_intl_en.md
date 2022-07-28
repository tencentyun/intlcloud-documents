Anycast CLB is a load balancing service that supports multi-region dynamic acceleration. Anycast CLB VIP is published in multiple regions. The client connects to the nearest POP and forwards access traffic to CVM through the high-speed internet of Tencent Cloud IDC.
Anycast CLB can optimize network transfer and achieve multi-entry nearby access, reducing network jitter and packet loss. It improves the service quality of applications on the cloud, expands the service scope, and streamlines backend deployment.
>?The feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Anycast CLB Architecture
Anycast CLB VIP is published in multiple regions. The client connects to the nearest POP and forwards the access traffic to CVM through the Tencent Cloud private network at high speed. For Anycast CLB regions, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/644/12617).
![]()


## Restrictions
The Anycast capability of Anycast CLB is implemented by binding an Anycast EIP to a private network CLB instance. For restrictions, see [Binding Private Network CLB to EIP](https://intl.cloud.tencent.com/document/product/214/44336).

## Prerequisites
This feature is in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Operation Guide
1. Log in to the [EIP console](https://console.cloud.tencent.com/cvm/eip?rid=1), select a region in the top-left corner of the **EIP** page, and click **Apply**.
2. In the **Apply for EIP** pop-up window, select **Accelerated IP** as the IP address type, set the bandwidth limit cap, click **I agree to Tencent Cloud EIP Service Agreement and Overdue Payment Policy**, and click **OK**.
3. Log in to the [CLB console](https://console.cloud.tencent.com/clb), select a region in the top-left corner of the **Instance Management** page, select the target private network CLB instance in the instance list, and click **More** > **Bind EIP** in the **Operation** column.
4. In the **Bind EIP** pop-up window, select the accelerated IP created just now and click **Submit**.
![]()
5. The private network CLB instance can provide Anycast CLB service after bound to an Anycast-accelerated IP. For more information on CLB configuration, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
![](https://main.qcloudimg.com/raw/f8e1334deb5679de7b5330208782a5e4.png)


## References
- [Anycast Internet Acceleration](https://intl.cloud.tencent.com/document/product/644)
- [Binding Private Network CLB to EIP](https://intl.cloud.tencent.com/document/product/214/44336)

