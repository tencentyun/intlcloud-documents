## Overview

This document describes the troubleshooting methods and solutions for when you receive a “ping unreachable” event alarm notification from CVM. You can resolve an alarm as instructed in [Troubleshooting Directions](#paichabuzhou). If you feel disturbed by the alarm notifications, you can [disable the alarm feature](#guanbi).

## Causes of the Alarms and their Corresponding Solutions

The causes of the “ping ureachable” alarms and their corresponding solutions are detailed below:

| Cause of the Alarm | Solution |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| CVM instance failure, kernel failure, or high bandwidth load | Troubleshoot as instructed in [Step 1](#buzhou1) to fix the exception, or [disable the alarm feature](#guanbi). |
| CVM instance shutdown | Troubleshoot as instructed in [Step 2](#buzhou2) to start the CVM instance, or [disable the alarm feature](#guanbi). |
| ICMP restricted in the security group associated with the CVM instance | Troubleshoot as instructed in [Step 3](#buzhou3) to modify the ICMP configuration of the security group, or [disable the alarm feature](#guanbi). |
| ICMP restricted by Windows Firewall or <br>the Linux kernel parameter or the iptables of the CVM instance | Troubleshoot as instructed in [Step 4](#buzhou4) to lift the corresponding restriction, or [disable the alarm feature](#guanbi). |

>?The network ping status of a CVM instance is automatically monitored by the alarm system of Cloud Monitor, which is irrelevant to whether a public IP is configured for the CVM instance.

<span id="paichabuzhou"></span>

## Troubleshooting Directions

<span id="buzhou1"></span>

### Step 1: Check the CVM instance monitoring data

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor). 
2. Click **Cloud Virtual Machine** > **ID/CVM Name** of the alarm to view whether there are exceptions such as breakpoints or overly high metric values in the CVM instance monitoring data.
	- If there are breakpoints or overly high metric values in the monitoring data, it might be due to CVM instance kernel failures, instance failures, or high bandwidth load. You can troubleshoot the problem as instructed in [Instance Related Failures](https://intl.cloud.tencent.com/document/product/213/12771).
	![](https://main.qcloudimg.com/raw/c0bac0a5e0ec3e7a2f95b3ebd0a94a36.png)
	- If everything is okay, please proceed to the next step to [check whether the CVM instance status has an exception](#cvmstate).

<span id="buzhou2"></span>

### Step 2: Check the CVM instance status

  > ?Currently, the “ping unreachable” alarms caused by manual shutdown are not excluded from the Cloud Monitor event alarms, which will be optimized in the future.

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index). 
 2. On the "Instances" page, check whether the status of the instance related to the “ping unreachable” alarm is normal.
- If the status is "shut down", the “ping unreachable” alarm was caused by manual shutdown. You can click **More** > **Instance Status** > **Start up** to restart the instance. If the instance status is "running" but the problem persists, you can proceed to the next step to [check whether ICMP is enabled in the security group associated with the CVM instance](#buzhou3).
 ![](https://main.qcloudimg.com/raw/1c8845adbc6c43f682c46d605f2eb507.png)
- If the status is "running", you can proceed to the next step to [check whether ICMP is enabled in the security group associated with the CVM instance](#buzhou3).

<span id="buzhou3"></span>

### Step 3: Check the ICMP settings in the security group

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the "Instances" page, select the ID/name of the instance where the “ping unreachable” alarm was triggered to access the instance details page.
3. Select the **Security Groups** tab to access the security group management page of the instance. Then, check whether the ICMP port protocol is refused or allowed in the inbound and outbound rules of the security group of the instance, as shown below:
   ![](https://main.qcloudimg.com/raw/84b612929b2078f08a3ef63d1f2ea519.png)
   - The ICMP port protocol is allowed in the system default security group. If you manually refuse the ICMP protocol in the default security group or do not add the ICMP protocol in the custom security group, the “ping unreachable” alarms will be triggered. You can click **Edit rule** in the top-right corner to add/modify the ICMP port protocol on the security group rule management page, as shown below:
     ![](https://main.qcloudimg.com/raw/de0c99ed1d34c2d49c7d8b15df3cbe40.png)
   - If the ICMP port protocol restriction in the security group has been modified but the problem persists, please proceed to the next step to [check whether there are restrictions in the CVM instance Windows firewall or the Linux kernel parameter and the iptables settings](#buzhou4).

<span id="buzhou4"></span>

### Step 4: Check the firewall or the Linux kernel parameter and the iptables settings

#### Windows 

1. Log in to the [CVM instance](https://intl.cloud.tencent.com/document/product/213/4855).
2. Open **Control Panel**, select "Small icons" as the view mode, and click **Windows Firewall**, as shown below:
   ![](https://main.qcloudimg.com/raw/f34c0cd664453a8340ff5787d67c7c3f.png)
3. On the "Windows Firewall" page, select **Advanced settings** as shown below:
   ![](https://main.qcloudimg.com/raw/4a4b6262f17db9816c8c3cdc57e7ca83.png)
4. In the "Windows Firewall with Advanced Security" window that pops up, check whether the ICMP inbound/outbound rules are restricted.
As shown below, if the "WinAgent:ICMP" inbound/outbound rules are disabled, the “ping unreachable” alarm was caused by the restriction in the Windows Firewall. You can right-click the rules to enable them.
    ![](https://main.qcloudimg.com/raw/2cc44ea785a598b540cce7d21613448c.png)

#### Linux 

>? Whether pings are allowed on Linux is subject to both the kernel and the iptables settings. If either of them disables pings, the “ping unreachable” alarms will be triggered.

**Check the kernel parameter**

1. Log in to the [CVM instance](https://intl.cloud.tencent.com/document/product/213/4855).
2. Run the following command to view the `icmp_echo_ignore_all` settings of the system:
```plaintext
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
- If 0 is returned, the system allows all ICMP echo requests. In this case, please [check the iptables settings](#CheckLinuxIptables).
- If 1 is returned, the system rejects all ICMP echo requests, which indicates that the “ping unreachable” alarm was caused by the restriction in the Linux kernel parameter. In this case, please enable ICMP as instructed in step 3.
3. <span id="Linux_step03">Run the following command using an account with root privileges to modify the settings of the `icmp_echo_ignore_all` kernel parameter:</span>
```plaintext
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxIptables"></span>

**Check the iptables settings**

1. Run the following command to check whether the current firewall rules of the CVM instance and the corresponding ICMP rules are restricted:
```plaintext
iptables -L
```
	- If the returned result is as follows, ICMP is not restricted in iptables:
		![](https://main.qcloudimg.com/raw/4edec2beb0d2cc175dddadd64ca6c51f.png)
	- If the returned result is as follows, ICMP is restricted in iptables, which indicates that the “ping unreachable” alarm was caused by the ICMP restriction in Linux iptables. In this case, please enable ICMP in iptables as instructed in step 2.
	![](https://main.qcloudimg.com/raw/004ce1d45e02a4dc5faa2ad0d3c56a9d.png)
<span id="LinuxIptables"></span>
2. Run the following command to enable ICMP in iptables:
```plaintext
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

If the problem persists after all the steps above are completed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

<span id="guanbi"></span>

## Disabling the Alarm Feature

### Disabling the alarm policy

If you feel disturbed by the metric alarms or the event alarms of an alarm policy, you can disable the policy by following the steps below:

1. Access the [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) page in the Cloud Monitor Console.
2. Find the name of the alarm policy that triggered the alarm, toggle off the switch in the **Alarm On/Off** column, and click **OK** to disable the alarm policy.
   ![](https://main.qcloudimg.com/raw/f8aae14afc04d22eec9326bf8eab9bcc.png)

### Only disabling event alarms

If you only need the metric alarms in an alarm policy, you can disable the event alarms by following the steps below:

1. Access the [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) page in the Cloud Monitor Console.
2. Click the name of the alarm policy that triggered the alarm to access the alarm policy management page.
3. Click **Edit** in the top-right corner of the “Trigger Condition” section. In the pop-up window, uncheck “Event Alarm” and click **Save** as shown below:
   ![](https://main.qcloudimg.com/raw/aac1c806476983d7c1e57572cf07d0c7.png)


