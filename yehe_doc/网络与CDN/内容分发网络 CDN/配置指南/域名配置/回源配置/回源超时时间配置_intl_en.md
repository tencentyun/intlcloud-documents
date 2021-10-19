## Configuration Scenario
When Tencent Cloud CDN forwards a request to the origin server, the default timeout period for TCP connection is 5 seconds, and the default timeout period for data loading during origin-pull is 10 seconds. If the origin-pull duration exceeds the aforementioned time limits, failures will often occur.

You can adjust the timeout periods for origin-pull TCP connection and data loading according to your origin server data processing conditions and network environment so as to ensure normal origin-pull.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click the domain name to enter its configuration page. You will find the origin-pull timeout configuration on the **Origin Configuration** tab. By default:
- The TCP connection timeout period is 5 seconds.
- The origin-pull loading timeout period is 10 seconds.

![](https://main.qcloudimg.com/raw/061fef4060d6aae5d16b3522b23fbbea.png)

### Modifying the configuration
You can click **Edit** on the right to modify the corresponding timeout period as needed:
- The TCP connection timeout period can be set to 5–60 seconds.
![](https://main.qcloudimg.com/raw/f70013c886612ef4dc33c353d8612336.png)
- The origin-pull loading timeout period can be set to 5–60 seconds.
![](https://main.qcloudimg.com/raw/e9c2cf6344275d477272ab2ba8c7e3b0.png)

>If your acceleration domain name is configured for global acceleration, the configured origin-pull timeout period will take effect globally. This configuration does not distinguish between requests from Mainland China and from outside Mainland China.

