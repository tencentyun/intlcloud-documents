### What should I do if consumption is exceptional?
- View whether traffic throttling is performed. Check whether there is a surge in traffic in Barad and upgrade the instance specification for solution.
- Check whether the limit of consumer groups has been reached.
- If rebalancing occurs frequently for network reasons, we recommend you adjust the client timeout period.
- Check whether expired offsets are pulled. Messages will be deleted after expiration, and if they are pulled with expired offsets, the pull will fail.

### What should I do if an error persists after a period of production?
- View whether traffic throttling is performed. Check whether there is a surge in traffic on the monitoring page and upgrade the instance specification for solution.
- View whether capacity throttling is performed. Check the instance capacity on the monitoring page and upgrade the instance specification or modify the data retention period for solution.


### How is the number of remaining unconsumed messages calculated?

Number of unconsumed messages = max offset position - submitted offset position, as shown below:

![](https://main.qcloudimg.com/raw/0583ce6cf94860b55b2823b20d6aec30.png)
