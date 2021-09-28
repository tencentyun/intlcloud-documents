 When connecting non-website applications such as PC games, mobile games and apps to DDoS Edge Defender, you need to configure port-based forwarding rules, which is described in this guide.

 ## Prerequisites
You have purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance.

## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Applications** on the left sidebar, and then click **Configure Now** at the bottom of the port-based access page.
![](https://main.qcloudimg.com/raw/e05e5c3ac29774380fba446574ccc460.png)
2. On the instance setting page, select an associated instance ID and then click **Next: Select Protocol**.
![](https://main.qcloudimg.com/raw/36b46616e32c1b44d2546c038d3ec8f4.png)
3. On the protocol setting page, select a forwarding protocol prior to clicking **Next: Set Port Parameter**.
![](https://main.qcloudimg.com/raw/d78eb1001864a5ff67d4b5f96764297c.png)
4. On the port parameter setting page, enter your application domain, and click **Next: Set Forwarding Method**.
>?The forwarding port and real server port must be an integer in the range 1–65535.

![](https://main.qcloudimg.com/raw/093d1057f4991ddff26f6064e1ea49c9.png)
5. On the forwarding method setting page, enter the configuration parameters, and click **Next: *Modify Resolution*.
![](https://main.qcloudimg.com/raw/435cd4aa61b3662f9164cdd2bdd32adb.png)
6. Modify the DNS resolution to complete the whole configuration.
