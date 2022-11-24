You can adjust the configuration of a purchased private engine. You don't need to adjust the configuration of public engines as they are managed by the system in a unified manner.

## Notes
You can adjust the configuration of a data engine only if it has no running tasks or is suspended. The engine will be unavailable during configuration adjustment and will be restarted automatically after the adjustment is completed.

## Adjusting the Configuration of a Monthly Subscribed Engine
You can adjust the CU configuration of a monthly subscribed private engine in the [Data Lake Compute console](https://console.cloud.tencent.com/dlc). For more information, see [Managing Private Data Engine](https://www.tencentcloud.com/document/product/1155/48684).

### Configuration upgrade billing rules
- The price difference for upgrading the configuration of a data engine should be made up based on the number of days. Configuration upgrade fees = price difference for upgrade per month * number of months for upgrade.
	- Price difference for the upgrade per month: Unit price difference between the new and old configurations.
		- Configuration upgrade fees are calculated by the number of days. Number of days for upgrade = resource expiration time - current time
		- Number of months for upgrade = number of days for upgrade / (365/12)
- Configuration upgrade doesn't affect the resource expiration time.
- You can pay configuration upgrade fees by using your vouchers and free credits.

### Configuration downgrade billing rules
Refund for data engine configuration downgrade = fees of original specification - fees of new specification. For more information, see [Refund](https://www.tencentcloud.com/document/product/1155/48653).
- If the refund is greater than 0, the configuration will be downgraded, and fees will be returned to your Tencent Cloud account accordingly.
- If the refund is less than or equal to 0, the configuration will be downgraded, but no fees will be refunded.
- If you use a discount or voucher for purchase, the discount amount and voucher will not be refunded.

## Adjusting the Configuration of a Pay-As-You-Go Engine
You can adjust the CU configuration of a pay-as-you-go private engine in the Data Lake Compute console. For more information, see [Managing Private Data Engine](https://www.tencentcloud.com/document/product/1155/48684). After the adjustment operation is submitted, the cluster status will become **Changing configuration**. After the adjustment is completed, the engine will be billed in pay-as-you-go mode based on the new configuration.