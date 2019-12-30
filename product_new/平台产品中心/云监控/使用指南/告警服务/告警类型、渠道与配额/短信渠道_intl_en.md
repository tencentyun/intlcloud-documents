## SMS Quota

Currently, Tencent Cloud SMS alarm channel has quote limit. The quota system consists of a free quota and an additional quota that you purchase.

When the monthly free SMS quota is used up, the system will send you an alarm notification, which will no longer be sent through the SMS channel for the rest of the month, but the email channel is not affected.

You can purchase an additional SMS quota if the free quota does not meet your needs.

## Quota Types

| Quota Type | Description |
| -------- | ---------------------------------------------------- |
| Free Quota | A certain amount of free SMS quota is available, allowing you to receive alarm notifications through the SMS channel |
| Additional Quota | You can purchase an additional SMS quota if the free quota does not meet your needs |

## Free quota details

| Alarm Type | Free Quota | Free Quota Granting Logic |
| -------------- | ------------ | ------------------------------------------------------- |
| Basic Alarm | 1,000 messages/month | The free quota is reset to 1,000 on the first day of each month, regardless of the remaining quota in the previous month |
| Cloud automated testing alarm | 1,000 messages/month | The free quota is reset to 1,000 on the first day of each month, regardless of the remaining quota in the previous month |
| Custom message alarm | 1,000 messages/month | The free quota is reset to 1,000 on the first day of each month, regardless of the remaining quota in the previous month |
| Custom monitoring alarm | 1,000 messages/month | The free quota is reset to 1,000 on the first day of each month, regardless of the remaining quota in the previous month |

## Additional quota details

### Billing methods of additional quotas

Additional quotas for different alarm types are calculated separately, so you need to purchase separate quotas for basic alarms, cloud automated testing alarms, custom message alarms, and custom monitoring alarms.

Currently, additional quotas are not available for custom message alarms or custom monitoring alarms.

| Additional quota to be purchased | Additional quota price |
| ---------------- | ------------ |
| < 100 messages | 0.055 |
| ≥ 100 messages and < 500 messages  | 0.052 |
| ≥ 500 messages and < 1,000 messages  | 0.050 |
| ≥ 1,000 messages | 0.045 |

>?
> - Deduction rule: When sending alarm messages, the system uses the free quota first, and then the additional quota if free quota is used up.
> Quota validity: An alarm quota is permanently valid. You can use a purchased quota at any time.

### Purchase Channels

Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/overview). On the **Monitoring Overview** page, you can view the SMS utilization. Click **Purchase SMS** to purchase an additional SMS quota.

## Quota counting rules

1. The quotas for each alarm type are counted separately. Each developer has a certain free SMS quota for each alarm type every month. When the free SMS quota for an alarm type is used up, it does not affect the SMS message sending of other alarm types.
2. The quantity deducted from an SMS quota is determined by the actual number of received messages. For example, if you configure 10 recipients to receive a certain alarm message (a total of 10 messages will be sent to 10 recipients when the alarm is triggered), 10 messages will be deducted from the corresponding SMS quota.

> ! Assume that you are using the repeated alarm notification feature, a recipient group of 10 recipients is configured for a certain alarm, and the alarm is configured to be sent repeatedly every hour. If the alarm lasts for 24 hours, 240 messages (10 x 24) will be deducted from the SMS quota. Note that repeated alarm notification increases SMS quota consumption.

3. When sending alarm messages, the system uses your free quota first, and then the additional quota if the free quota is used up.
