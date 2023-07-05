## Configuration Overview

Tencent Cloud CDN supports configuring User-Agent (UA) blocklist/allowlist rules for access control.
CDN checks the `User-Agent` field in HTTP request headers based on the rules to allow or reject user access requests.

## Configuration Guide

### Configuration limitations

- The blocklist and allowlist cannot be set at the same time. Please set either the blocklist rules or the allowlist rules.
- Maximum number of blocklist/allowlist rules: 10
- Rules support the wildcard `*`. Please separate multiple values with `|`.
- Supported effect types: all content, file extension, file directory, and specified file. Regular matching is currently not supported.

### Configuration instructions

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and then click **Manage** on the right of a domain name to enter its configuration page. Select **Access Control** tab to find the UA blocklist/allowlist configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/07914bd30b3d422fb4bddf3a323d92f2.png)
When the switch is toggled off, click **Add Rule** to add blocklist/allowlist rules one by one:
![](https://main.qcloudimg.com/raw/66d3fc72f575efaa4ae42382d8fde179.png)

>!
>1. Only the wildcard `*` is supported; other regular expressions are not supported.
>2. If there is no `*`, all characters will be used for exact match.

The overall configuration will be disabled after a rule is added, so the ongoing services will not be affected:
![](https://main.qcloudimg.com/raw/679129885ec36329178e87af671d6743.png)
You can toggle the switch on to officially deploy the configured UA blocklist/allowlist.
![](https://main.qcloudimg.com/raw/fd85de8e702b24e7d2eaaf8b34667c95.png)

## Configuration Samples

The UA blocklist/allowlist configuration of `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/c7e06060bc627aab2e4939b53460951d.png)
If `User-Agent` in the HTTP request header is as follows:

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.61 Safari/537.36
```

The blocklist will be hit and a 403 error will be directly returned.

