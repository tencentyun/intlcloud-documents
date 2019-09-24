## What if a production/consumption error occurs after a new client is connected to the service?

- Check whether telnet works. It might be a network issue. Check if Kafka and the producer are in the same network.
- Check whether the accessed vip - port is correctly configured.
- Check whether the topic is whitelisted. If yes, you need to configure the correct IP for access.

## What if no messages can be seen when testing with the client in the Kafka console?
-If the “latest” option is used, consumer can only get the last messages, and production needs to be ongoing in order to see the corresponding messages.
-Change to the "earliest" option for data consumption.

## What if an error persists after a period of production?
- View whether traffic control is performed. Check whether there is a surge in traffic on the monitoring page and upgrade the instance specification for solution.
- View whether capacity control is performed. Check the instance capacity on the monitoring page and upgrade the instance specification or modify the data retention period for solution.

## Traffic Control Descriptions
-	Traffic control is at the instance level and affects all topics in the instance.
-After the full capacity is reached, consumption can continue but production cannot.
-Traffic = actual traffic \* number of replicas.
-Accumulation = actual accumulation (replica accumulation is also counted).

## Consumption Exceptions
-	View whether traffic control is performed. Check whether there is a surge in traffic in Barad and upgrade the instance specification for solution.
-Check whether the number of consumer groups exceeds the limit.
-If rebalance occurs frequently due to network reasons, we recommend adjusting the client timeout period.
-	Check whether expired offsets are pulled. Messages will be deleted after expiration, and if they are pulled with expired offsets, the pull will fail.

