1. The number of elastic nodes reaches the lower limit. To continue scale-in, you can adjust the minimum number of nodes allowed.
Cause: The scale-in rule is triggered, but the current number of elastic nodes is smaller than the minimum number of nodes allowed.
Solution: To continue scale-in, reset the minimum number of nodes allowed.

2. The number of elastic nodes reaches the upper limit. To continue scale-out, you can adjust the maximum number of nodes allowed.
Cause: The scale-out rule is triggered, but the current number of elastic nodes is equal to the maximum number of nodes allowed.
Solution: To continue scale-out, reset the maximum number of nodes allowed.

3. Scale-out is impossible because no scaling specification is configured. You can add a scaling specification and try again.
Cause: The auto scaling rule is triggered, but no node specification is added in the **Auto-scaling** > **Scaling Specification Management** section in the console, as shown in the figure above.
Solution: Click **Add Specification** in the top-right corner and select the required node specification.

4. Scaling cannot be performed due to insufficient resources. You can switch to a specification with sufficient resources or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.
Cause: The scale-out rule is triggered but the selected specification has insufficient resources in the current availability zone.
Solution: Switch to a node specification with sufficient resources.

5. The current retry period upon expiration is too short. We recommend extending the retry period.
Cause: The scaling rule is triggered, but there are other auto scaling processes in the cluster, which prevent the rule from being executed within current retry period upon expiration.
Solution: Edit the rule to extend the retry period upon expiration to ensure that the rule can be executed.
6. Scale-out cannot be performed due to insufficient account balance.
Cause: The scale-out rule is triggered, but the account balance is insufficient at the time when an order is placed.
Solution: Go to the [Billing Center](https://console.cloud.tencent.com/expense/overview) to top up your account.
7. No eligible elastic resources are available for scale-in.
Cause: The scale-in rule is triggered, but no elastic nodes are available currently or timed termination is set for all nodes.
Solution: Perform manual scale-in for nodes that are set to be terminated at a certain time.
8. The cluster is not in a scalable state.
Cause: The scale-out rule is triggered, but the cluster is not running due to component installation, previously triggered scale-out, or other factors.
Solution: Perform manual scale-out or edit the rule to extend the retry period upon expiration to ensure that the rule can be executed.
9. The cluster is in a cooldown period and scale-out cannot be triggered for the moment. We recommend adjusting the cooldown period for scaling rules.
Cause: The scale-out rule is triggered, but the cluster is in a cooldown period due to other scaling processes.
Solution: Shorten the cooldown period for other scaling rules or extend the retry period upon expiration for the current scale-out rule.
