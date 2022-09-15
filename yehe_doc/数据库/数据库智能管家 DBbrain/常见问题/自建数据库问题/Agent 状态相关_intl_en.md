
### How do I view the agent status?
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance?product=mysql) and select **Instance Management** on the left sidebar. On the displayed page, select a database type at the top, and you can view the agent status in the displayed list.


### What should I do if the agent is abnormal?
- If you find that the agent connection is abnormal on the instance management page, enter the following command on the server to check the agent process:
   ```
ps aux|grep dbbrain-agent
   ```
- If there is no output, the agent has stopped unexpectedly. You need to go to the agent installation directory on the server and then restart the agent by running the following commands:
   ```
cd /path/to/dbbrain-agent
./bin/start.sh
   ```
If `Successfully start agent` is output, the start succeeded.

