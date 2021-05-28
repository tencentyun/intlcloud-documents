### What should I do if no messages can be seen when testing with the client in the Kafka console?
-	If the "latest" option is used, consumer can only get the last messages, and production needs to be ongoing in order to see the corresponding messages.
-	Change to the "earliest" option for data consumption.


### What should I do if a production and/or consumption error occurs after a new client is connected to the service?
- Check whether telnet works. It might be a network issue. Check whether Kafka and the producer are in the same network.
- Check whether the accessed vip - port is correctly configured.
- Check whether the topic allowlist is enabled, and if so, you need to configure the correct IP for access.
