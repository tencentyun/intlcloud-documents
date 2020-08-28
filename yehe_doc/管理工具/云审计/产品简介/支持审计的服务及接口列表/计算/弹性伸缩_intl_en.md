Tencent Cloud Auto Scaling (AS) provides efficient policies for managing computing resources. With AS, you can set intervals to regularly execute management policies. You can also create real-time monitoring policies to automatically add or remove CVM instances based on the real-time needs and deploy the instance environment, so as to ensure the stable operation of your business and minimize costs. With auto scaling policies, applications with stable and regular needs can be automatically managed, enabling you to get rid of problems such as business traffic surges and CC attacks; resources for applications with irregular needs can also be expanded within minutes based on the business load, keeping the number of instances in your cluster always appropriate.

AS operations supported by CloudAudit are as shown below:

| Operation Name	| Resource Type | Event Name |
|----------------|----------------------------------------|----------------|
| Adding CVM instance to scaling group  | as                      | AttachInstances |
| Completing lifecycle action       | as              | CompleteLifecycleAction |
| Creating scaling group          | as               | CreateAutoScalingGroup |
| Creating launch configuration         | as            | CreateLaunchConfiguration |
| Creating lifecycle hook       | as                  | CreateLifecycleHook |
| Creating notification           | as      | CreateNotificationConfiguration |
| Creating alarm trigger policy       | as                  | CreateScalingPolicy |
| Creating scheduled task         | as                | CreateScheduledAction |
| Deleting scaling group          | as               | DeleteAutoScalingGroup |
| Deleting launch configuration         | as            | DeleteLaunchConfiguration |
| Deleting lifecycle hook       | as                  | DeleteLifecycleHook |
| Deleting notification           | as      | DeleteNotificationConfiguration |
| Deleting alarm trigger policy       | as                  | DeleteScalingPolicy |
| Deleting scheduled task         | as                | DeleteScheduledAction |
| Querying scaling activity         | as        | DescribeAutoScalingActivities |
| Querying the last scaling activity of scaling group  | as | DescribeAutoScalingGroupLastActivities |
| Querying scaling group          | as            | DescribeAutoScalingGroups |
| Querying instance           | as         | DescribeAutoScalingInstances |
| Querying launch configuration         | as         | DescribeLaunchConfigurations |
| Querying lifecycle hook       | as               | DescribeLifecycleHooks |
| Querying notification           | as   | DescribeNotificationConfigurations |
| Querying alarm trigger policy       | as              | DescribeScalingPolicies |
| Querying scheduled task         | as             | DescribeScheduledActions |
| Removing CVM instance from scaling group  | as                      | DetachInstances |
| Disabling scaling group          | as              | DisableAutoScalingGroup |
| Enabling scaling group          | as               | EnableAutoScalingGroup |
| Triggering scaling policy         | as                 | ExecuteScalingPolicy |
| Modifying scaling group          | as               | ModifyAutoScalingGroup |
| Modifying the desired capacity        | as                | ModifyDesiredCapacity |
| Modifying launch configuration attribute       | as  | ModifyLaunchConfigurationAttributes |
| Modifying the CLB instance of scaling group    | as                  | ModifyLoadBalancers |
| Modifying notification           | as      | ModifyNotificationConfiguration |
| Modifying alarm trigger policy       | as                  | ModifyScalingPolicy |
| Modifying scheduled task         | as                | ModifyScheduledAction |
| Deleting CVM instance from scaling group | as                      | RemoveInstances |
| Setting instance removal protection       | as               | SetInstancesProtection |
| Disabling CVM instance in scaling group  | as             | StopAutoScalingInstances |
| Upgrading lifecycle hook       | as                 | UpgradeLifecycleHook |
