The allowlist feature is used to allow specified users to report more information. To filter out certain users and reduce the number of user API requests, RUM provides this feature and configures its logic.
The allowlist logic is as follows:

1. For users in the allowlist, all API information will be reported, including API request and response.
2. For users in the allowlist, the `info` API can be used to report data.
3. `info` and `infoAll`: in the actual development experience, for users in the allowlist, more logs can be added and reported with the `info` API. `infoAll` reports the data of all users without discrimination; therefore, it may result in a large volume of log data.
4. You can use the `whitelist` API to check whether the current user is in the allowlist, and if so, the response (aegis.isWhiteList) of the user will be bound to the Aegis instance for your use.
5. To reduce your workload, the allowlist takes effect at the business system level. You can go to **Application Management** > [**Allowlist Management**](https://console.cloud.tencent.com/rum/web/group-whitelist-manage) to create an allowlist, and it will take effect for all applications in the current business system.