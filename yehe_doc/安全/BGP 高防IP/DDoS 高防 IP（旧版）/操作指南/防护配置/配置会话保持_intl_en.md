## Operation Scenarios
The non-website business protection service of Anti-DDoS Advanced provides IP-based session persistence to support forwarding requests from the same IP address to the same real server for processing.
Layer-4 forwarding supports simple session persistence. The session persistence duration can be set to any integer between 30 and 3600 seconds. If the time threshold is exceeded and the session has no new request, the connection will be automatically closed.
## Directions
The following describes how to configure a session persistence rule for non-website business protection in Anti-DDoS Advanced.
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Anti-DDoS Advanced** > **Access Configuration** on the left sidebar to enter the management page.
2. On the **Non-Website Business** tab, select the target Anti-DDoS Advanced instance and the corresponding rule, and click **Edit** in the "Session Persistence" column.

3. On the **Edit Session Persistence** page, click <img src="https://main.qcloudimg.com/raw/4fc9677c00fe017208bf6f049d3892c4.png"  style="margin:0;"> to enable session persistence, set the persistence duration, and click **OK**.
>
>- Session persistence is disabled by default.
>- When setting the persistence duration, you are recommended to use the default value.
>- The session persistence configuration information can be imported and exported in batches. After import, the system will match the rules one by one according to the imported "forwarding protocols and forwarding ports", and the "forwarding ports" must have rules configured.
