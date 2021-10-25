After purchasing an SCDN package, log in to the [SCDN Console](https://console.intl.cloud.tencent.com/cdn/scdn) to add and configure your domain name. Your defense configurations for the domain name will be deployed to all SCDN nodes, which does not affect your business.

## Creating a Distribution

On the **Defense Settings** page, click **Create a Distribution**.

![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbiq5g7lwj62540cc76a02.jpg)

The distribution creation page consists of two parts:

- Basic defense configuration
- Custom defense policy

### Basic defense configuration

This feature allows you to configure the web attack defense, CC attack defense, and DDoS attack defense settings for your domain name.

![](https://tva1.sinaimg.cn/large/008i3skNgy1gvblkqghl5j60au08pwem02.jpg)

- Protected domain name

  - Select one or more domain names to connect to SCDN (wildcard domain names are not supported).
  - The domain name you select must be already connected to CDN and the CDN service is enabled.
  - Up to 10 domain names can be added at a time. The total number of domain names connected to SCDN cannot exceed the limit of your SCDN package.

- Web attack defense

  ![](https://tva1.sinaimg.cn/large/008i3skNgy1gvbllxn8knj60l5050dfw02.jpg)

  - You can enable web attack defense as needed.
  - Defense mode: supports **Block** and **Observe** modes. The **Block** mode enables SCDN nodes to detect web attack requests and block them based on your setting, returning the default blocking page and a 403 status code, or redirecting the requests to your custom blocking page.
  - Custom page address: the user-defined page to which SCDN nodes redirect the web attack requests.
  - Redirect status code: supports status codes 301 and 302.

- CC and DDoS attack defense

  - CC attack defense and DDoS attack defense are enabled by default.
  - Elastic defense will be enabled by default if your package includes the service. Otherwise, it is disabled by default. For more details, see [Billing](https://intl.cloud.tencent.com/document/product/1032/42540).

### Custom defense policy

SCDN allows you to create complex access control rules by specifying fields, such as IP, URI, Referer, User-Agent and Params, to filter requests. You can also create and combine multiple conditions with the condition logic in a single rule depending on the business scenario. ![](https://tva1.sinaimg.cn/large/008i3skNgy1gvblp56xkij60wf06k74l02.jpg)![](https://tva1.sinaimg.cn/large/008i3skNgy1gvblq4rg28j60l90cqt9602.jpg)

- Defense rule
  - A maximum of five custom rules can be created and each rule can have up to five matching conditions. These rules and conditions are combined with OR and run in order from top to bottom. **If any of these conditions is met, the access is blocked**.
  - Match field: supports Params, URL (only limited to path, such as `/test/1.jpg`, excluding parameters after "?"), IP (client IP), Referer, and User-Agent.
  - Match condition: supports Include, Exclude, Equal to, Not equal to, Length shorter than, Length equal to, and Length longer than.
  - Match value: supports only **one** match, and does not support regular expressions. It is left blank by default if not specified.

### Submitting configuration

Click "Submit" to submit your completed domain name configuration, which takes about five minutes to be effective. In the pop-up window, click **Back to Defense Configuration** if you want to return to view or modify your configuration; click **Continue** if you want to add domain names.