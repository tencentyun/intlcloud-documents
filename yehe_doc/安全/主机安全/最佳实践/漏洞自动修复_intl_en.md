This topic describes the best practices for automatically fixing vulnerabilities.

>! Auto-fixing of vulnerabilities may involve executing commands on your servers, which may affect running applications or core system components, and restarting applications or operating systems, which may affect your business continuity. For servers that are used for your core business, we recommend that you take the impact into full consideration when planning which vulnerabilities to fix and in what order to do so.

## Limitations
- Supported servers: CVM Ultimate on which CWPP is online.
- Supported vulnerabilities: Linux software vulnerabilities (some) and Web-CMS vulnerabilities (some).

## Operation Guide
1. Log in to the [CWPP Console](https://console.cloud.tencent.com/cwp) and click **Vulnerability Management** in the left navigation pane. Then the list of detected vulnerabilities is shown at the bottom.
2. The vulnerabilities in the **Vulnerability List** are categorized as Urgent Vulnerabilities, Critical Vulnerabilities, and All Vulnerabilities, which are discovered vulnerabilities that are not obviously different from each other in terms of functionality. The steps for fixing vulnerabilities automatically are described below using **All Vulnerabilities** as an example.
>?
>- Priorities: Urgent vulnerabilities > Critical vulnerabilities > All vulnerabilities.
>- For vulnerabilities that can be automatically fixed, **Auto Fix** is shown in the operation column; for vulnerabilities that cannot be automatically fixed, **Fix Scheme** is shown in the column.

![](https://qcloudimg.tencent-cloud.cn/raw/42e2c0585bd59bcff68e62c72a05db4a.png)

### Step 1: View vulnerability details
Click **Auto Fixi** to open the vulnerability details pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/99e488c40c1701b21bb93d73bf51b524.png)

### Step 2: Select the servers for which you want to fix vulnerabilities automatically.
Select the target servers in the affected server list, and click **Fix** to open the confirmation pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/9cdc6b2a6114e88188919b852bc374f7.png)

### Step 3: Choose whether to create snapshots
Click **Confirm** to open the fix method configuration pop-up window, and select the fix method: Fix and Automatically Create Snapshots, or Fix Without Creating Snapshots
![](https://qcloudimg.tencent-cloud.cn/raw/723aa164a00d133222d5445683b8b0af.png)

- Fix and Automatically Create Snapshots: You can set the snapshot name and snapshot storage duration (3 days, 7 days, or 15 days). It is recommended to set the duration to 7 days so that the snapshots can be rolled back in time if necessary.
- Fix Without Creating Snapshots: If snapshots have been created for all the servers selected for fixing vulnerabilities on the current day, this item becomes optional.

### Step 4: Fix vulnerabilities
Click **Confirm** to start fixing the vulnerabilities. You can keep track of the process.
![](https://qcloudimg.tencent-cloud.cn/raw/c384f8ecd30af4a43466567e976d9e85.png)

### Step 5: Check the server status changes
Return to **Vulnerability Details** to check the server status changes. If vulnerability fixing fails, the status is "Fixing Failed"; if vulnerability fixing is successful, the status changes to "Fixed".
![](https://qcloudimg.tencent-cloud.cn/raw/19cdf6e71382aa2673337adfdbe123e3.png)

- After the vulnerabilities are fixed, if your business is greatly affected, click **Rollback** to go to **[CVMs](https://console.cloud.tencent.com/cvm/instance/index?rid=1)** > **Snapshot List**, and then select the snapshots created before the fixing to roll back them. After the rollback is successful, restart the servers to scan the vulnerabilities again.
- After the vulnerabilities are fixed, perform a **Rescan** to verify whether the vulnerabilities have been fixed.
- You can also click "Fix Details" to view the details of fixing.

 
