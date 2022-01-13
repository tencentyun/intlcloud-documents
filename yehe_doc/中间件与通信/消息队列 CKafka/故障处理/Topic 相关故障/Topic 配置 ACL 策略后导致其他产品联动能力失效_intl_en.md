## Issue Description

The linkage capabilities of other Tencent Cloud services fail after an ACL policy is configured for a topic.

## Possible Causes

By default, no ACLs are set for a topic, and the topic can be accessed without limit by instances in the same VPC. If you want to control the permissions in the VPC, you can configure an ACL as instructed in [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).

When you add an ACL policy for a topic, the policy will prevent all other ineligible requests from accessing the topic, including those initiated by other Tencent Cloud services connected to CKafka (e.g., log shipping in CLS, message dump in SCF, and component consumption in EMR).

From a business point of view, the business wants to ensure that clients that don't meet the requirements cannot access Kafka data once an ACL is set; therefore, the rejection is reasonable.

## Solutions

Before adding an ACL policy for a topic, you must determine whether the topic is being used in other scenarios through the service information or the monitoring information in the console; otherwise, problems with other linked features may occur.

In such cases, if you have to use an ACL policy, we recommend you produce messages to a new topic for permission grant instead of reusing the original topic.









