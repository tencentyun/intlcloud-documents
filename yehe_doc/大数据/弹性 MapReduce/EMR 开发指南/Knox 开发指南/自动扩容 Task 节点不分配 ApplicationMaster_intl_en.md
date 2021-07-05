## Overview
In the automatic scaling scenario, when a scale-in rule is triggered, if an ApplicationMaster (AM) is running on the task node to be terminated, the running AM will also be terminated, which will cause the current job to fail.

## Features
No AMs will be assigned to the task nodes added via automatic scaling that are achieved by the transformation of YARN source code and the addition of configuration items to the automatic scaling process. Instead, all AMs will be assigned to those that are not automatically added. Automatically added task nodes are responsible for compute tasks only. In this case, an automatic scale-in action will only terminate the nodes processing compute tasks, while the AMs remain active and will try to take over the compute tasks on other nodes to keep the current job running.

## Application Scope
1. Only applies to task nodes added via automatic scaling.
2. Only available for EMR v2.0.1 and EMR v3.1.0.
