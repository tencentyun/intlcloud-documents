CMQ meets the three key needs of Qidian.com operated by China Literature:

 1. In the **Zhangyishucai** operation system, consumer crediting in the feature of grabbing red packet monthly tickets is async. The credit information will be first written to a message queue and then pulled by the consumer. After the consumer confirms that the message is successfully consumed, the callback API will delete the message from the queue.

 2. In another scenario, major systems of Qidian.com such as OPS, alarming, and operations generate massive volumes of logs. The logs will be first aggregated into CMQ, and the backend big data analysis clusters will continuously pull them out of CMQ and analyze them based on the processing capabilities. CMQ can theoretically retain an unlimited number of messages, bringing you complete peace of mind when using it.

 3. A feature similar to message rewind in Kafka is provided. After business consumption is successfully completed and the messages are deleted, message rewind can be used to consume the deleted messages again. The offset position can be specified for flexible adjustment. This feature facilitates Qidian.com in reconciliation and business system retry.

The overall business of Qidian.com presents high pressure on CMQ, as the API request QPS exceeds 100,000, and the total number of daily requests exceeds 1 billion. CMQ can easily support Qidian.com with high stability under such huge business pressure.

The CMQ backend cluster is imperceptible to users, and the CMQ controller server can schedule and relocate queues in real time based on the load of the cluster. If the request volume of a queue exceeds the service threshold of the current cluster, the controller server can distribute the queue routes to multiple clusters to increase the number of processable concurrent requests. In theory, CMQ can achieve unlimited message retention and extremely high QPS.
