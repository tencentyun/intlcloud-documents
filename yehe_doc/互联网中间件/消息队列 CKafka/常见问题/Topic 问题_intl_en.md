### What should I do if the linked capabilities of other Tencent Cloud services fail after an ACL policy is configured for a topic?
When you add an ACL policy for a topic, the policy will prevent all other ineligible requests from accessing the topic, including those initiated by other Tencent Cloud services connected to CKafka (e.g., log shipping in CLS, message dump in SCF, and component consumption in EMR). Therefore, before adding an ACL policy for a topic, you must determine whether the topic is being used in other scenarios through the service information or the monitoring information in the console; otherwise, problems with other linked features may occur.

In such cases, if you have to use an ACL policy, we recommend you produce messages to a new topic for permission grant instead of reusing the original topic.


### How do I choose an appropriate number of CKafka replicas?
To ensure data reliability, you are recommended to choose two or three replicas for data storage when creating a topic. Currently, CKafka has banned the creation of single-replica topics. If you have a single-replica topic in your account, please migrate it as follows:

1. Create a topic, select the same partition parameter, and select "dual-replica";
2. Produce messages in the new topic while the existing single-replica topic continues to be consumed;
3. Modify the consumer configuration after consumption is completed to subscribe to the new topic for consumption.
