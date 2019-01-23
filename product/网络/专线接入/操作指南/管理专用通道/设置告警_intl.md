You can configure alarms for a Dedicated Tunnel. The configuration steps are as follows:
1. Open [Cloud Monitoring - Alarm Policy Console](https://console.cloud.tencent.com/monitor/policylist).
2. Enter the alarm policy name.
3. Click **Add** and edit the alarm policy:
 - Select "Dedicated Tunnel" for "Policy Type".
 - Select "Outbound Bandwidth", "Inbound Bandwidth", "Packet Loss", and "Latency" for "Alarm Triggering Conditions".
4. Click **Next: Associate Alarm Object**, and select the associated Dedicated Tunnel.
5. Set the **Alarm Receiver Group**, and then click **OK** to complete the alarm policy configuration.

After the Dedicated Tunnel alarm is configured, you can receive the system alarm according to the setting of the alarm receiving group. For more information on monitoring, please see [Cloud Monitoring](https://cloud.tencent.com/doc/product/248/967).
