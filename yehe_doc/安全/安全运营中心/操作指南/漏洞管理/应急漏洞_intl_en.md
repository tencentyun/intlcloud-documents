Security Operation Center can detect the urgent vulnerabilities that are exposed to the Internet suddenly. The Urgent Vulnerability page displays the vulnerabilities recently exposed. You can use the urgent vulnerability detection feature provided by Vulnerability Management under Security Operation Center to detect your assets in real time to confirm whether any assets are affected.

## Prerequisites

To view and test the urgent vulnerabilities feature, you must have enabled [Security Operation Center Premium](https://buy.cloud.tencent.com/soc).

## Directions

1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/vulner/urgent) and click **Vulnerability Management** in the left navigation pane.
2. On the Vulnerability Management page, click **Urgent Vulnerabilities** to go to the Urgent Vulnerabilities page.
3. On the Urgent Vulnerabilities page, you can view all vulnerability alerts, locate a vulnerability by entering its name or ID, and filter vulnerabilities by vulnerability type, risk level, and detection time.
   Description of the status of recent detection results:

- **Detecting**: Detection is being performed.
- **The selected detected server has no risk**: No such vulnerability was detected on the server.
- **n assets with vulnerability**: After detection is completed, the system will count the number of assets with such vulnerability, if any. If you click on the number of assets "n", a navigation drawer that bears vulnerability details appears on the right side. Then you can ignore assets or fix the vulnerability as instructed there.

  > ! Once ignored, the selected server will no longer be detected when your Cloud Workload Protection (CWP) detects the vulnerability. You cannot unignore these ignored assets.

- **No detection**: When the Security Operation Center has set operation rules for urgent vulnerabilities, if no detection is performed for such vulnerabilities, "No detection" is displayed in the Recent Detection Results column. When no operation rules are set for the same, "One-Click Detection" is not supported, and "--" is displayed in the Recent Detection Results column.

4. All vulnerabilities that meet the filter criteria will appear in the vulnerability list below.

- **One-Click Detection**: You can perform one-click detection on some urgent vulnerabilities. If any vulnerability risks are detected, the number of risks will be updated in the vulnerability list.

  > ! The one-click detection feature for urgent vulnerabilities only performs attack-free proof of concept testing, during which you need to install the [CWP Agent](https://console.cloud.tencent.com/cwp/asset/machine/install). If not installed, you will not be able to use the feature.

  1. In the list of urgent vulnerabilities, select the target vulnerability, click **One-Click Detection** in the operation pane on the right, and check the "Agree to the security detection agreement" option to go to the One-Click Detection page.
  2. On the One-Click Detection page, select a detection target to start detection. The detection targets include "All servers" and "Partial servers". After you select a detection target, click **Start Detection**. If any vulnerability risks are detected, the number of risks will be updated in the vulnerability list.

- **Viewing vulnerability details**: You can select the target vulnerability in the list of urgent vulnerabilities and click **View Details** in the operation pane on the right to open vulnerability intelligence.
