You can implement backend web services by writing SCF functions and bind them with CLB instances to provide services.

## Background
Tencent Cloud [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583) is a serverless execution environment that enables you to build and run applications without having to purchase and manage servers. After creating a function, you can create a CLB trigger to bind the function and event. The CLB trigger will pass the request content as parameters to the function and return the result from the function back to the requester as the response.

## Overview
<dx-accordion>
::: \sHTTP/HTTPS\s\sgeneral\saccess
Applicable to apps for ecommerce, social media and other services, and web applications for personal blogging, event pages and more. The workflow is as follows:
1. HTTP/HTTPS requests initiated by apps, browsers, H5 pages, or Mini Programs access the SCF function through the CLB instance.
2. After the CLB instance completes the certificate uninstallation, SCF only needs to provide HTTP services.
3. The request is then transferred to the SCF function for subsequent processing, such as writing to the cloud database and calling other APIs.
![](https://main.qcloudimg.com/raw/534ca758662eaffdd40d243bd8384739.svg)
:::
::: Switching\sbetween\sCVM\sand\sSCF
Applicable to migrating HTTP/HTTPS services from CVM to SCF, especially in the event of failover. The workflow is as follows:
1. The app, browser, H5, or Wechat Mini Program initiates an HTTP/HTTPS request.
2. The request is then resolved to two CLB instances’ VIPs by the DNS.
3. One CLB instance forwards the request to the CVM and the other forwards it to the SCF.
4. The switch from CVM to SCF on the backend is complete without affecting the client side.
![](https://main.qcloudimg.com/raw/d285c006b5945486a725936385d9dcb2.svg)
:::
::: CVM/SCF\s\sbusiness\sdiversion
Applicable to using SCF to handle highly elastic services and CVM to handle daily business in scenarios such as flash sales and snap-up purchase.
1. Through DNS resolution, domain name A is resolved to one CLB instance’s VIP and domain name B is resolved to the other CLB instance’s VIP.
2. One CLB instance forwards the request to the CVM and the other forwards it to the SCF.
![](https://main.qcloudimg.com/raw/96a77f06ecad23ddf13282aa2e6a496b.svg)
:::

</dx-accordion>



## Restrictions
- Binding with SCF is only available in Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Tokyo, and Silicon Valley.
- SCF functions can only be bound with CLB instances of bill-by-IP accounts but not with bill-by-CVM accounts. If you are using a bill-by-CVM account, we recommend upgrading it to a bill-by-IP account. For more information, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246). 
- SCF functions cannot be bound with classic CLB instances.
- SCF functions cannot be bound with classic network-based CLB instances.
- SCF functions in the same region can be bound with CLB instances. SCF functions can only be bound across VPCs but not regions.
- SCF functions can only be bound with IPv4 and IPv6 NAT64 CLB instances, but currently not with IPv6 CLB instances.
- SCF functions can only be bound with layer-7 HTTP and HTTPS listeners, but not with layer-7 QUIC listeners or layer-4 (TCP, UDP, and TCP SSL) listeners.
- Only SCF event functions can be bound with CLB instances.


## Prerequisites
1. You have created a [CLB instance](https://intl.cloud.tencent.com/document/product/214/6149).
2. You have configured an [HTTP](https://intl.cloud.tencent.com/document/product/214/32515) or an [HTTPS](https://intl.cloud.tencent.com/document/product/214/32516) listener.

## Directions
![](https://main.qcloudimg.com/raw/eca21ba71ea22a6c240d3b4a05dfdce0.svg)

### Step 1. Create a function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. On the **Function Service** page, click **Create**.
3. On the **Create** page, select **Custom** for the creation mode, and enter a function name. Then select the same region that you selected for your CLB instance and **Python3.6** for the runtime environment, enter the following code in the input box (Hello CLB is used for illustration), and click **Complete**.
>!When you bind your CLB instance to the SCF function, content needs to be returned in the specific response integration format. For more informantion, see [CLB Trigger](https://intl.cloud.tencent.com/document/product/583/39849).
```plaintext
# -*- coding: utf8 -*-
import json
def main_handler(event, context):

    return {
        "isBase64Encoded": False,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html"},
        "body": "<html><body><h1>Hello CLB</h1></body></html>"
   }
```

### Step 2. Deploy the function
1. On the "Functions" list page, click the name of the function you created.
2. On the **Function Management** page, select the **Function Codes** tab and click **Deploy** at the bottom.
![]()

### Step 3. Bind the function
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. On the **Instance Management** page, click **Configure Listener** on the right of an instance.
3. In the **HTTP/HTTPS Listener** section, select the listener to be bound with an SCF function. Click the **+** icon on the left of the listener and the domain name under it, select the URL path displayed, and click **Bind**.
![]()
4. In the pop-up window, select SCF as the target type, set the configuration items, and click **Confirm**.
![]()
5. On the **Listener Management** tab, you should see the function bound to the CLB instance in the **Forwarding Rules** section, indicating the CLB trigger is created.
![]()
>? You can also create a CLB trigger in the SCF console to bind the CLB instance with an SCF function. For more information, please see [Creating Triggers](https://intl.cloud.tencent.com/document/product/583/31441).

## Result Validation
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. On the **Function Service** page, click the function you just created.
3. Click **Trigger Management** on the left.
4. On the **Trigger Management** page, click the **Access Path**.
![]()
5. Open the access path in a browser. If "Hello CLB" is displayed, the function is successfully deployed.
![]()


## References
[Creating functions using the console](https://intl.cloud.tencent.com/document/product/583/32742)
