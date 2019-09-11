## What if the production/consumption is exceptional after a new client is connected to the service?

- Check whether telnet works (there may be a network issue. The Ckafka instance should reside in the same network environment as the producer).
- Check whether the accessed vip - port is correctly configured.
- Check whether the topic whitelist is enabled. If yes, you need to configure the correct IP for access.

## What if no data can be seen during test with the client in the CKafka Console?
-	If the "latest" option is used, the consumer can only get the last data, and production should be maintained at the same time for it to see the corresponding data.
-	Changed to the "earliest" option for data consumption.

## What if an error persists after a period of production?
- View whether traffic control is performed. Check whether there is a surge in traffic on the monitoring page and upgrade the instance specification for solution.
- View whether capacity control is performed. Check the instance capacity on the monitoring page and upgrade the instance specification or modify the data retention period for solution.

## Traffic Control Descriptions
-	Traffic control is at the instance level and affects all topics in the instance.
-	After the full capacity is occupied, consumption can continue but production cannot.
-	Traffic = actual traffic \* number of replicas
-	Accumulation = actual accumulation (replica accumulation is also counted)

## Exceptions with Consumption
-	View whether traffic control is performed. Check whether there is a surge in traffic in Barad and upgrade the instance specification for solution.
-	Check whether the consumer group exceeds the quantity limit.
-	If rebalance is triggered frequently due to network reasons, it is recommended to adjust the client timeout period.
-	Check whether expired offsets are pulled. Messages will be deleted after expiration, and if they are pulled with expired offsets, the pull will fail.

