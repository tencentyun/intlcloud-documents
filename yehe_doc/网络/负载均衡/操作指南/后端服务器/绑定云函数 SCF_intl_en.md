You can implement backend web services by writing SCF functions and bind them with CLB instances to provide services.
>? Binding CLB instances with SCF functions is currently in beta. If you want to use it, please submit an application.
>

## Background
Tencent Cloud [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583) is a serverless execution environment that enables you to build and run applications without having to purchase and manage servers. After creating a function, you can create a CLB trigger to bind the function and event. The CLB trigger will pass the request content as parameters to the function and return the result from the function back to the requester as the response.

## Use Cases

#### Typical scenario 1: Flash sales
Flash sales have high requirements for the application flexibility of the overall resource, and are closely related to the main business scenarios. SCF is generally a relatively independent module in a business system, which is convenient for migration and transformation. You can seamlessly apply SCF through CLB. For billing based on the number of service calls, the overall pricing and migration costs are relatively lower. In addition, cross-origin resource sharing over the same domain name can be easily achieved.
![](https://main.qcloudimg.com/raw/9407d48ee26c116a59c26c83e3f8c9db.png)

#### Typical scenario 2: Auxiliary system architecture
SCF can be applied with CLB for your web businesses, such as the order system, data collection system, BI analysis, and other minor business scenarios in which the traffic peak shifting is important, enabling a cost-effective business migration.
![](https://main.qcloudimg.com/raw/414fc87fbcc391912d42261a8347bf15.png)

#### Typical scenario 3: Dynamic and static resource separation
When the number of requests is high, targeted distribution of requests to the website can be achieved by differentiating the static and dynamic requests, effectively reducing the backend load pressure. The dynamic requests can be processed by separately deployed CLB instances and associated SCF functions; while the static content can be connected to CDN and optimized by COS to significantly improve the loading speed.
![](https://main.qcloudimg.com/raw/910ee56aac139ead66be7dae556ca6e2.png)

#### Typical scenario 4: Domain name access differentiation based on regions
For businesses highly related to regions, you can use CLB instances to differentiate access based on regions for SCF.


## Restrictions
- SCF functions can only be bound with CLB instances of bill-by-IP accounts but not with bill-by-CVM accounts. If you are using a bill-by-CVM account, we recommend upgrading it to a bill-by-IP account. For more information, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246). 
- SCF functions cannot be bound with classic CLB instances.
- SCF functions cannot be bound with classic network CLB instances.
- SCF functions can only be bound across VPCs but not across regions.
- SCF functions can only be bound with IPv4 and IPv6 NAT64 CLB instances, but currently not with IPv6 CLB instances.
- SCF functions can only be bound with layer-7 HTTP and HTTPS listeners, but not with layer-7 QUIC listeners or layer-4 (TCP, UDP, and TCP SSL) listeners.

## Prerequisites
1. Create a [CLB instance](https://intl.cloud.tencent.com/document/product/214/6149).
2. Configure an [HTTP](https://intl.cloud.tencent.com/document/product/214/32515) or an [HTTPS](https://intl.cloud.tencent.com/document/product/214/32516) listener.

## Operation Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb).
2. On the **Instance Management** page, click **Configure Listener** on the right of an instance.
3. In the **HTTP/HTTPS Listener** section, select the listener to be bound with an SCF function. Click the **+** icon on the left of the listener and the domain name under it, select the URL path displayed, and click **Bind**.
![](https://main.qcloudimg.com/raw/15cd2745ad1a5eb5708cc822d4a55cfa.png)
4. In the pop-up window, select SCF as the target type, set the configuration items, and click **Confirm**.
![](https://main.qcloudimg.com/raw/12286261c9c84316b4634fce0ee5aa96.png)
5. On the **Listener Management** tab, click the function name in the **Forwarding Rules** section.
![](https://main.qcloudimg.com/raw/2da69c0e92fe34a744a48c4a8c7cdb05.png)
6. Edit the function code on the **Function Code** tab. Content needs to be returned in the specific response integration format. For more information, please see [CLB Trigger](https://cloud.tencent.com/document/product/583/52635#.E9.9B.86.E6.88.90.E5.93.8D.E5.BA.94).
![](https://main.qcloudimg.com/raw/d0560171044434579e07b8dbcc963c10.png)
>? You can also create a CLB trigger in the SCF console to bind the CLB instance with an SCF function. For more information, please see [Creating Triggers](https://intl.cloud.tencent.com/document/product/583/31441).

## Documentation
[Creating functions using the console](https://intl.cloud.tencent.com/document/product/583/32742)
