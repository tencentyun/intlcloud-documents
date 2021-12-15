This document describes how to install an agent.

## Prerequisites

- You have created a TMP instance.
- You have created an agent.

## Directions
1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance and click **Agent Management** on the left.
3. Click the agent ID to enter the agent installation guide page, copy the agent installation command to your CVM instance or self-built IDC, modify the `<secret_id>` and `<secret_key>` in the command, and run it.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3c867c8aa996e9a223605e82b35be454.png)
   Below is an example of successful execution:
   ![](https://main.qcloudimg.com/raw/9737c22b742419eb798f5dfa8bdb84d0.png)
4. Return to the agent management page. If the agent is running normally, you can see the version, IP address, and heartbeat time reported by the agent.

## Other Commands

### Restarting agent
Run the following command:
```
systemctl restart prometheus
```

### Stopping agent
Run the following command:

```
systemctl stop prometheus
```

### Checking agent status
Run the following command:

```
systemctl status prometheus
```

### Viewing agent log
Run the following command:

```
journalctl -f --unit=prometheus
```

### Uninstalling agent
Run the following command:
```
systemctl stop prometheus && rm -rf /usr/lib/systemd/system/prometheus.service
```

