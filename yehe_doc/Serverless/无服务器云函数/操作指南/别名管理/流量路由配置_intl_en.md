## Operation Scenarios
Serverless Cloud Function (SCF) allows you to configure traffic routing. With this feature, you can easily control the beta launch or rollback process in actual use cases or environments in order to avoid the risks that may be brought by direct launch.

When creating an alias or adjusting the traffic configuration, you can point the traffic to two function versions in the console, so that the traffic can be routed between versions by the specified rule. Currently, two routing schemes are supported, namely, **random routing by weight** and **routing by rule**.
 - If you want to randomly route requests to any two versions by the specified weight in percentages, you can configure [random routing by weight](#RandomRoutingByWeight).
 - If you want to route requests containing certain content to the specified version, you can configure [routing by rule](#RoutingByRule).


## Directions
### Random routing by weight<span id="RandomRoutingByWeight"></span>
This document uses configuration during alias creation as an example to describe how to configure routing. After the alias is created, traffic will be randomly routed to two versions by the specified percentages. The steps are as follows:

1. Enter the "Create Alias" window.
2. In the "Create Alias" window, configure traffic routing based on the information below:
![](https://main.qcloudimg.com/raw/e8e388f7f432c30e11865a20224513e7.png)
Main parameters include:
 - **Routing Method**: select **By weight**.
 - **Version Weight Configurations**: you can select two versions in the drop-down lists and set their weights in percentage.
5. Click **Submit** to complete the settings.





### Routing by rule<span id="RoutingByRule"></span>
The current rule syntax for routing by rule consists of the following three parts:

- **Match key**<span id="matchKey"></span>
	It is the position of the value to be read during the match and is used to determine whether the rule is hit.
	The key should be in the format of `invoke.headers.[userKey]` where `[userKey]` can be modified. This format indicates that when the `invoke` API is called, the `userKey` part in `headers` of the HTTP request will be used for match.
- **Match method**<span id="matchMethod"></span>
	During the match, the expression is compared in a specified method. Currently, the `exact` and `range` match methods are supported.
	* `exact`: exact match. When the `exact` method is used, the match expression should be a string. If the value read through the match key is exactly the same as the expression, the rule will be hit.
	* `range`: range match. When the `range` method is used, the match expression should be in the format of `(a,b)` or `[a,b]` where `a` and `b` need to be integers. If the value read through the match key is an integer in the range specified by the expression, the rule will be hit.
- **Match expression**<span id="matchExpression"></span>
If the specified value is matched, it will be considered as a hit. For more information on how to compose an expression, please see the description in [Match Method](#matchMethod).



You can configure routing by rule in the following steps:

1. Enter the "Create Alias" window.
2. In the "Create Alias" window, configure traffic routing and click **Submit** to complete the configuration as shown below:
![](https://main.qcloudimg.com/raw/6b2eb645608c9f9a05264aa491e40580.png)
Main parameters include:
 - **Routing Method**: select **By rules**.
 - **Version Rule Configurations**: set the fields as needed based on the following example:
    1. For example, if you have two versions (version 2 and version 1) and want to set the match rule of version 2 to `invoke.headers.User exact Bob` and set that of version 1 to "miss", you can set the fields as shown below:
![](https://main.qcloudimg.com/raw/24bda8565dec51bf2f96fc9f2a1842fc.png)
According to the configuration, when SCF invokes the function alias through the `invoke` API, if the `routingKey` parameter is set to `{"User":"Bob"}`, version 2's code and configuration will be used during this execution; if the `routingKey` parameter is not set or set to another value, version 1's code and configuration will be used.
    2. For example, if you have two versions (version 3 and version 2) and want to set the match rule of version 3 to `invoke.headers.userHash range [1,50]` and set that of version 2 to "miss", you can set the fields as shown below:
    ![](https://main.qcloudimg.com/raw/a3e4da8c3134c69c820d14fc534d7b17.png)
		According to the configuration, when SCF invokes the function alias through the `invoke` API, if the `routingKey` parameter is set to `{"userHash":30}`, version 3's code and configuration will be used during this execution; if the `routingKey` parameter is not set or set to another value such as `{"userHash":80}`, version 2's code and configuration will be used.

