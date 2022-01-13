## Issue Description
Consumption data is exceptional.

## Troubleshooting Approaches

- You can view the traffic monitoring data on the monitoring page in the CKafka console to check whether there is a surge, and if so, upgrade the instance specification for solution.
  ![](https://main.qcloudimg.com/raw/a5ef5e5067c265073ef8cb0c07960461.png)

- Check whether the limit of consumer groups has been reached.

- If rebalancing occurs frequently for network reasons, we recommend you adjust the client timeout period.

- Check whether expired offsets are pulled. Messages will be deleted after expiration, and if they are pulled with expired offsets, the pull will fail.

