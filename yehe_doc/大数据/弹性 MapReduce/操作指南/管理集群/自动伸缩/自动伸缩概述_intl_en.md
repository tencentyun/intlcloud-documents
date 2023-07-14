## Overview
You can configure scaling rules in EMR to automatically increase or reduce the computing resources of task nodes as your cluster load changes. This saves costs while quickly responding to changes in the computing needs. Automatic scaling supports two scaling policies: load-based scaling (for YARN-enabled clusters only) and time-based scaling.

## Notes
1. Automatic scaling is disabled by default. It can be either custom scaling or managed scaling. Currently, managed scaling is made available through an allowlist. To use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
2. Custom scaling can be either load-based or time-based. If you switch the scaling policy, the original scaling rules will be retained. However, they will be in an invalid state and will not be triggered or executed. The added nodes will be retained unless the scale-in rule is triggered.
3. In managed scaling, only **HOST** is supported as the resource type; in custom scaling, **HOST** and **POD** are supported and cannot be used at the same time. If you switch the resource type, the resource specification and instance deployment methods set for the original resource type will be retained. However, they will be in an invalid state and will not be triggered or executed. The added nodes will be retained unless a scale-in rule is triggered. Pod resources are currently made available through an allowlist. To use them, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
4. **Pay-as-you-go** and **Spot instances preferred** are supported as the instance deployment policies. However, Pod resources can be deployed only on a pay-as-you-go basis.

