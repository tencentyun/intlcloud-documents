#### Limits on pushing notifications of all channels
- Self-built Channel: Full push messages with the same content can only be sent once an hour, and there is no limit to the frequency and number of send times for other push targets.
- Vivo Push Limits
The daily limit of single push and group push is calculated based on the number of SDK subscriptions. When < 10000, it is counted as 10000; when > 10000, it is equal to the number of SDK subscriptions. One push can be sent daily by default. For details, see [vivo official document](https://dev.vivo.com.cn/documentCenter/doc/156)
- OPPO Push Limits
When the cumulative number of users < 50,000, the push limit is 100,000; when >= 50,000, the push limit is 2 * the cumulative number of users.
The cumulative number of users can be queried at  [OPPO Push Operation Platform](https://push.oppo.com), and will be refreshed daily.
- MEIZU Platform Limits
	1. There is a rate limit for the push of a single application. The default value is 500 messages per second.
	2. There is a limit to the number of pushes per day for a single application. The default value is 1000 times per day.
	3. No more than 100 tags for a single application subscription 
	4. When messages sent to a device for a single application >= 4, they will be collapsed. The messages may be stored in the upper right corner without clicking for several times. 
	5. Subscription will be cancelled after a device is inactive for 1 month.
	6. There is a limit on the number of API requests for one IP address per hour. MEIZU has not given a specific number yet.
	7. There is a limit to the accumulated number of API requests for a single application per day. MEIZU has not given a specific number yet.
	8. There is a limit to the total number of messages that a single application can push per day. MEIZU has not given a specific number yet.
    
- HUAWEI Platform Limits
	1. Push number limit: The number of messages sent to a single device can not exceed 3,000 per day. After exceeding the limit, the rate will be limited for 24 hours. When more than 100,000 pieces are pushed to a single device within a day, the push authorization will be stopped. You should rectify and provide a rectification plan to HUAWEI to get push authorizations again.
	2. Push speed limit: HUAWEI Push allocates the push speed mainly based on two factors: monthly activity of the application on HUAWEI channels and app type when the application is launched in the HUAWEI App Store.
	
- MI Platform Limits
XIAOMI Push Service does not set any limits to the push frequency. The data size of one notification should be smaller than 4 KB.


 **Guide of Usage Excess** If the amount of notifications pushed through the platform channel exceeds the limit of the day, the push task after the excess will be reissued through the self-built channel.



