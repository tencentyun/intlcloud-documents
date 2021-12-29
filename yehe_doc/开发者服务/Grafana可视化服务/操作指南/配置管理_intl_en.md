TCMG allows you to customize the Grafana configuration parameters, LDAP configuration parameters, and environment variables.


## Prerequisites

1. Log in to the [TCMG console](https://console.cloud.tencent.com/monitor/grafana).
2. Find the target instance and click **Instance ID**.

## Grafana Configuration

1. Enter the instance details page and click **Configuration** in the list on the left.
2. On the **Configuration** management page, click **Create** in the top-left corner.
   ![](https://qcloudimg.tencent-cloud.cn/raw/2245fd15ef317a41798ba9cafa4c8cde.png)
3. In the pop-up window, enter the custom configuration file content in INI format, click **Save**, and the instance will be rebooted. For more information, see [Configuration](https://grafana.com/docs/grafana/latest/administration/configuration/#config-file-locations).

## LDAP Configuration
1. Enter the instance details page and click **Configuration** in the list on the left.
2. On the **Configuration** management page, switch to the **LDAP Configuration** tab and click **Modify** in the top-left corner.
3. Enter the custom LDAP configuration content in INI format as instructed in [LDAP Authentication](https://grafana.com/docs/grafana/latest/auth/ldap/#grafana-ldap-configuration), click **Save**, and the instance will be rebooted.

## Environment Variable
1. Enter the instance details page and click **Configuration** in the list on the left.
2. Switch to the **Environment Variable** tab and click **Modify** in the top-left corner.
3. Configure the environment variable as needed, click **Save**, and the instance will be rebooted.
   ![](https://qcloudimg.tencent-cloud.cn/raw/11a2f6582147eaeebc7b021d1fd286a7.png)

## Notes
1. Currently, you cannot configure credentials for LDAP.
2. The environment variable name must start with a letter or underscore and can contain only letters, underscores, and digits.
