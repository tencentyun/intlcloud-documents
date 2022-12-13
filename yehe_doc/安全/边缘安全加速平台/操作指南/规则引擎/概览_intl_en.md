## Overview
The rule engine leverages rich rule languages to customize rules for specified request types. Custom policies in the rule engine will overwrite the default behaviors of the edge server.

## Use Cases
- Site-level configuration in **Site Acceleration** cannot cover all business conditions. Different subdomain names, paths, or file extensions require differentiated configurations, and the feature configuration should be based on the specified request.
- Besides basic configurations such as cache and HTTPS, the current business also requires custom cache key, URL rewrite, HTTP header modification, and other acceleration features.

## Directions
1. Log in to the [EdgeOne console](https://console.tencentcloud.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and click **Add rule**.
3. In the pop-up window, configure parameters and submit the rule:
   - Save only: Saves the rule but does not publish it to the production environment.
   - Save and publish: Saves and publishes the rule to the production environment.

## Key Terms

| Definition       | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Rule       | A rule contains requests of a certain type and operations on them, including:<li>A set of conditional expressions to define the logic for identifying a request.</li><li>A set of conditions to define the standard for identifying a request.</li><li>A set of features to define how CDN processes requests.</li> |
| Conditional expression | It defines the logic for identifying a request and is available in the following types:<li>IF <br/>Note: An IF statement can be nested inside another IF statement, indicating that the nested one will be executed only after the other is met.</li><li>ELSE IF </li><li> ELSE |
| Condition   | It defines the standard for identifying a request, including:</li><li>Matching type </li><li> Operator </li><li>Value</li> |
| And/Or     | Logical AND/OR, which can link multiple conditions.                           |
| Operation       | A series of feature configurations applied to the hit request.                               |

## Priority

| Scope                                      | Description                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| Rule engine vs. site acceleration                      | The rule engine has a higher priority and is the configuration that eventually takes effect.                         |
| Single rule in the rule engine | Rules are executed from top to bottom in sequence. The bottom rule has a higher priority and is the configuration that eventually takes effect. |
| Multiple rules in the rule engine | Rules are executed from top to bottom in sequence. The bottom rule has a higher priority and is the configuration that eventually takes effect.<br>Note: You can place general or coarse-grained rules at the top as the default configuration and request-specific or finer-grained rules at the bottom. |

### Notes

Certain operations are not subject to the order, for example:

- Token authentication
  [Token authentication](https://intl.cloud.tencent.com/document/product/1145/46164) will be executed first no matter where it is placed. If a request hits two rules, token authentication will be executed first even if it is at the bottom, as other operations will be performed only after authentication is passed.
