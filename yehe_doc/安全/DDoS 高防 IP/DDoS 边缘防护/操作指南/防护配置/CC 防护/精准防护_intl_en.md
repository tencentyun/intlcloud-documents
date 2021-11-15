 DDoS Edge Defender supports precise protection for connected web applications. With the precise protection, you can configure protection policies combining multiple conditions of common HTTP fields, such as URI, UA, Cookie, Referer, and Accept to screen access requests. For the requests matched the conditions, you can configure CAPTCHA to verify the requesters or a policy to automatically drop the packets. Precise protection is available for policy customization in various use cases to precisely defend against CC attacks.

The match conditions define the request characteristics to be checked, i.e., the attribute characteristics of the HTTP field in a request. Precise protection supports checking the HTTP fields below:

| Field | Description                                               | Logic           |
| -------- | ------------------------------------------------------ | ------------------ |
| URI      | URL address of the access request                                    | Equal to; Include; Exclude |
| UA       | Information including identifier of the client browser that initiates the access request               | Equal to; Include; Exclude |
| Cookie   | Cookie information in the access request                         | Equal to; Include; Exclude |
| Referer  | Source website of the access request, from which the access request is redirected | Equal to; Include; Exclude |
| Accept   | Data type to be received by the client that initiates the access request                 | Equal to; Include; Exclude |



## Prerequisites
You have successfully purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance and set the object to protect.

>? DDoS Edge Defender is currently available to beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Protection Policy** on the left sidebar, and then select the tab **CC Protection**.
2. Select an Edge Defender instance ID, such as "edge-xxxxxxx".
![](https://main.qcloudimg.com/raw/e43f351d75409dd50d4add1a2fd266f2.png)
3. Click **Set** in the **Precise Protection** section on the right.
![](https://main.qcloudimg.com/raw/6b3a20abe36432a84dcf13ad11b72f0f.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields, and click **OK** to create a rule.
![](https://main.qcloudimg.com/raw/caa7012de385195ed0ccadca27955658.png)
6. Now the new rule is added to the rule list, you can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/8b67f586be6f6059f53fdcac50023fbe.png)
