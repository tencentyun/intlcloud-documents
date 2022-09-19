You can use the custom password strength feature with the root account or a sub-account granted with the corresponding CAM permissions. This document describes how to enable and disable the custom password strength feature.

## Version limits
The custom password strength feature is supported by the following versions:
- MySQL 5.7 on kernel minor version 2.0.21 or later and 2.1.7 or later.
- MySQL 8.0 on kernel minor version 3.1.7.

You can use this feature only after upgrading the kernel to the above versions. For detailed directions, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/1098/44617).

## Enabling custom password strength feature
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
3. On the cluster management page, select **Account Management** and enable **Custom Password Strength** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/6e39e810abecfa806efe966c9e7101e1.png)
4. In the pop-up window, click **Next** to enter the initial settings page.
![](https://qcloudimg.tencent-cloud.cn/raw/7f7be5d84d231020b37b83c46190c967.png)
5. Complete the following settings and click **OK**.
In the initial settings of the custom password strength feature, two scenarios will be displayed for different password strength levels.
Scenario 1: The password strength level is **MEDIUM**.
![](https://qcloudimg.tencent-cloud.cn/raw/88a06bfd036e4441c6f94e751c0e62a4.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Password Strength Level</td>
<td>You can select <b>MEDIUM</b> or <b>STRONG</b> as the strength level.<ul><li>MEDIUM: The feature under this setting will check the length, digits, letters, and symbols.</li><li>STRONG: The feature under this setting will check the length, digits, letters, symbols, and non-compliant word dictionary.</li></ul></td></tr>
<tr>
<td>Min Number of Uppercase and Lowercase Pair</td>
<td>The minimum number of pairs of uppercase and lowercase letters that the password must contain. For example, if this parameter is set to `2`, the password must contain at least two uppercase letters and two lowercase letters. Default value: `1`. Value range: 1–50.</td></tr>
<tr>
<td>Min Number of Digits</td>
<td>The minimum number of digits that the password must contain. Default value: `1`. Value range: 1–50.</td></tr>
<tr>
<td>Min Number of Symbols</td>
<td>The minimum number of special symbols that the password must contain. Default value: `1`. Value range: 1–50.</td></tr>
<tr>
<td>Min Password Length</td>
<td>The minimum length of the password. Default value: `8`. Value range: 8–256. This parameter equals to the number of digits + number of symbols + 2 * number of letters, and it must be greater than or equal to 8 for security of your password. If the final value after the sum of above parameters is greater than 8, it will be used as the minimum of the range.</td></tr>
</tbody></table>
Scenario 2: The password strength level is **STRONG**.

![](https://qcloudimg.tencent-cloud.cn/raw/2d4df5dbd9c20c86f06642f7f9e04dd7.png)

<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Password Strength Level</td>
<td>You can select <b>MEDIUM</b> or <b>STRONG</b> as the strength level.<ul><li>MEDIUM: The feature under this setting will check the length, digits, letters, and symbols.</li><li>STRONG: The feature under this setting will check the length, digits, letters, symbols, and non-compliant word dictionary.</li></ul></td></tr>
<tr>
<td>Min Number of Uppercase and Lowercase Pair</td>
<td>The minimum number of pairs of uppercase and lowercase letters that the password must contain. For example, if this parameter is set to `2`, the password must contain at least two uppercase letters and two lowercase letters. Default value: `1`. Value range: 1–50.</td></tr>
<tr>
<td>Min Number of Digits</td>
<td>The minimum number of digits that the password must contain. Default value: `1`. Value range: 1–50.</td>
</tr>
<tr>
<td>Min Number of Symbols</td>
<td>The minimum number of special symbols that the password must contain. Default value: `1`. Value range: 1–50.</td></tr>
<tr>
<td>Min Password Length</td>
<td>The minimum length of the password. Default value: `8`. Value range: 8–256. This parameter equals to the number of digits + number of symbols + 2 * number of letters, and it must be greater than or equal to 8 for security of your password. If the final value after the sum of above parameters is greater than 8, it will be used as the minimum of the range.</td></tr>
<tr>
<td>Non-Compliant Dictionary</td>
<td>If the password strength level is <b>STRONG</b>, this parameter is configurable. You can click <strong>Dictionary Settings</strong> for configuration. Each non-compliant word can contain 4–100 letters. After configuration, the system will check passwords for non-compliant words during password verification. If any non-compliant word (case-insensitive) is detected, the verification will fail.</td></tr>
</tbody></table>

## Disabling custom password strength feature
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
3. On the cluster management page, select **Account Management** and disable **Custom Password Strength** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/0207223c39e41042f2a68383a4a1fe2d.png)
4. In the pop-up window, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/bbcb300c0056e95f9a5a24c800374da2.png)
5. In the pop-up window, you can click **Batch Disable** to select other clusters with the custom password strength feature enabled and batch disable the feature.
>?
>- Once the custom password strength feature is disabled, the parameters you set will be automatically reset to the default value. If you enable the feature again, you need to configure these parameters again.
>- You can select up to 20 clusters in one batch disablement operation.

