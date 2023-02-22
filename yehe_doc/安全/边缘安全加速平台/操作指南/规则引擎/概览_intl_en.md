## Rule Engine
Leveraging rich rule languages, the rule engine allows you to customize rules for specific request types. Custom rules will overwrite the default behaviors of the edge server.

## Use Cases
- Provide custom configurations based on different conditions (subdomain name, path and file extension) when site-level configuration in **Site Acceleration** cannot meet your needs.
- Provide basic features (caching and HTTPS) and acceleration features (custom cache key, URL rewrite and HTTP header modification).

## Directions
1. Log in to the [EdgeOne console](https://console.tencentcloud.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and click **Add rule**.
3. In the pop-up window, configure parameters and submit the rule:
   - Save only: Saves the rule but does not publish it to the production environment.
   - Save and publish: Saves and publishes the rule to the production environment.

## Key Terms

| Term       | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Rule       | A rule identifies specific types of requests and the series of operations applied to them. It includes:<li>A set of conditional expressions that define the logic for request identification.</li><li>A set of conditions that define the criteria for request identification.</li><li>A set of features that define how CDN processes requests.</li> |
| Conditional expression | It defines the logic for identifying a request and is available in the following types:<li>IF <br/>Note: An IF statement can be nested inside another IF statement, indicating that the nested one will be executed only after the other is met.</li><li>ELSE IF </li><li> ELSE |
| Condition   | It defines the criteria for identifying a request, including:</li><li>Matching type </li><li> Operator </li><li>Value</li> |
| And/Or     | Logical AND/OR, which can link multiple conditions.                           |
| Operation       | A wide range of feature configurations that can be applied to hit requests.                               |

## Rule Precedence

| Scope                                      | Description                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| Rule engine                      | The rule engine takes precedence over the site acceleration configuration.                         |
| Single rule in the rule engine | Rules are executed from top to bottom in sequence. The bottom rule has a higher priority and is the configuration that eventually takes effect. |
| Multiple rules in the rule engine | Rules are executed from top to bottom in sequence. The bottom rule has a higher priority and is the configuration that eventually takes effect.<br>Note: You can place general or coarse-grained rules at the top as the default configuration and request-specific or finer-grained rules at the bottom. |

### Notes

The following operation is not subject to the execution order:

- Token authentication
  [Token authentication](https://intl.cloud.tencent.com/document/product/1145/46164) will be executed first no matter where it is placed. If a request hits two rules, token authentication will be executed first even if it is at the bottom, as other operations will be performed only after authentication is passed.
