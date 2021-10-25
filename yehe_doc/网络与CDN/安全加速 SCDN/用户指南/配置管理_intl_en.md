On the [SCDN console](https://console.cloud.tencent.com/cdn/scdn), you can view and modify your SCDN configurations such as web attack defense and custom defense policies. Your modification will take effect in about 5 minutes once submitted.

## Configuring a Domain Name

Log in to the [SCDN Console](https://console.cloud.tencent.com/cdn/scdn), locate the domain name to check or modify its configuration, and click **Manage**.

![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbm1vl670j612207ymxz02.jpg)

The domain name configuration page will display the security configuration details, including the web attack defense, DDoS attack defense and CC attack defense settings as well as custom defense policies.

![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbm2m9sw6j610v09saat02.jpg)

## Modifying the Configuration

On the domain name configuration page, you can modify the following defense settings based on your business needs.

### Web attack defense

Based on Tencent's massive web attack samples, SCDN supports identifying good access requests from bad ones and protecting your origin server against web attacks including SQL injection, XSS attacks and local file inclusion in real time. ![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbm3td1w8j611g05s3yl02.jpg)![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbm4ehxhzj60h308haa802.jpg)

- You can enable web attack defense and set defense levels as needed.
- Defense mode: supports **Block** and **Observe** modes. The **Block** mode enables SCDN nodes to detect web attack requests and block them based on your setting, returning the default blocking page and a 403 status code, or redirecting the requests to your custom blocking page.
- Custom page address: the user-defined page to which SCDN nodes redirect the web attack requests.
- Redirect status code: supports status codes 301 and 302.

### Custom defense policy

SCDN allows you to create complex access control rules by specifying fields, such as IP, URI, Referer, User-Agent and Params, to filter requests. You can also create and combine multiple conditions with the condition logic in a single rule depending on the business scenario. ![](https://tva1.sinaimg.cn/large/008i3skNgy1gvblp56xkij60wf06k74l02.jpg)![](https://tva1.sinaimg.cn/large/008i3skNgy1gvblq4rg28j60l90cqt9602.jpg)

1. Adding and modifying defense rules
   - A maximum of five custom rules can be created and each rule can have up to five matching conditions. These rules and conditions are combined with OR and run in order from top to bottom. **If any of these conditions is met, the access is blocked**.
   - Match field: supports Params, URL (only limited to path, such as `/test/1.jpg`, excluding parameters after "?"), IP (client IP), Referer, and User-Agent.
   - Match condition: supports Include, Exclude, Equal to, Not equal to, Length shorter than, Length equal to, and Length longer than.
   - Match value: supports only **one** match, and does not support regular expressions. It is left blank by default if not specified.
2. Disabling and deleting rules
   - By clicking **Enable**/**Disable**, you can enable/disable rules as needed.
   - By clicking **Delete**, you can delete rules as needed. The rules that you deleted cannot be restored.
3. Adjusting priority
   - By clicking **Adjust Priority**, you can adjust the rule order, without affecting blocking requests.

### DDoS and CC attack defense

With advanced feature recognition algorithms, SCDN delivers a precise cleansing of attack traffic and an all-round protection against DDoS attacks including SYN floods, TCP floods and ICMP floods. Meanwhile, it can analyze and block malicious CC attacks using self-designed intelligent CC attack identification and blocking technologies, recommended policies, and multi-dimensional, custom rules.

- CC attack defense and DDoS attack defense are enabled by default.
- Custom IP access limit rules are supported.

![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbm788ny2j611o0br3za02.jpg)

- Elastic defense will be enabled by default if your package includes the service. Otherwise, it is disabled by default. For more details, see [Billing](https://intl.cloud.tencent.com/document/product/1032/42540).