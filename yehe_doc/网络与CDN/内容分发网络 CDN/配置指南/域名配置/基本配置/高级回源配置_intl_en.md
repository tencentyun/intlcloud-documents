## Advanced origin-Pull configurations
Tencent Cloud CDN allows you to configure fine-grained origin-pull based on origin-pull rules, such as path-based rules (i.e., specifying a file type, folder, full file path, or homepage for origin-pull) and client IP region-based rules.

## Restrictions
By default, the origin-pull protocol and origin domain of the primary origin server are adopted for the advanced origin-pull configuration and cannot be modified.


## Configuration Guide

### Configuration in domain management
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn).
2. Click **Domain Management** on the left sidebar to enter the domain name management list.
3. Select the target domain name and click **Manage** to enter the domain name configuration page.
4. On the **Baisc information** tab, find the **Origin server** section and click **Edit** in the top-right corner of the **Primary origin** section.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fuBU862_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423162924.png)
5. Click **Advanced origin-pull configuration**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/a5wQ272_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423163046.png)
6. Set the configuration items in the **Advanced origin-pull configuration** section as described in the following table.

| Item | Description |
|--|--|
| Origin-pull Rule | Client requests can be forwarded by the following rules:<br>Client IP: This rule directs origin-pull requests of clients inside or outside the specified region to the specified origin address.<br>File extension: This rule directs origin-pull requests for the specified file extensions to the specified origin address. If you specify multiple file extensions, separate them with semicolons (;).<br>File directory: This rule directs origin-pull requests for files in the specified directory to the specified origin address. If you specify multiple directories, separate them with semicolons (;).<br>Full path: This rule directs origin-pull requests for a specific file with its full path, such as `/a/1.jpg`, to the specified origin address. If you specify multiple files with their full paths, separate the files with semicolons (;).<br>Homepage: This rule directs origin-pull requests for files on the homepage to the specified origin address. |
| Origin-pull Address | You can specify domain names or IP addresses. One origin-pull address is required for an origin-pull rule. In addition, the value of the origin domain specified for the primary domain name in the **Origin server** section is used. |
| Port | You can specify a custom origin-pull port number. If you do not specify custom port numbers, port 80 is used for origin-pull over HTTP and port 443 is used for origin-pull over HTTPS. The origin-pull protocol depends on settings of the origin server. If you select **HTTPS** for **Origin-pull Protocol** in the **Origin server** section, the requests hit by an advanced origin-pull rule are forwarded over HTTPS. |

### Configuration limitations
- Each domain name can be configured with up to 50 rules.
- The origin-pull address of a single rule can be an IP, domain name, and port (range: 0 - 65535; port can be omitted). If "HTTPS" or "Follow Protocol" is selected as the origin-pull protocol, the port should be 443 or left empty.
- More actions: you can adjust rule priority and edit or delete multiple rules in batches.

### Rule priorities
First, the priority of a client IP rule is lower than that of a path-based rule. Second, if multiple path-based rules are specified, rules at lower positions in the rule list have higher priorities.
For example, you have specified that origin-pull requests of clients from the Jiangsu region are forwarded to `1.1.1.1` and origin-pull requests for files whose path contains `/test` are forwarded to `2.2.2.2`. When a client from the Jiangsu region accesses `/test`, the origin-pull request is forwarded to `2.2.2.2`.

## Sample configuration
**Example:**
This example describes three origin-pull scenarios, assuming that you have configured `www.example.com` as the CDN acceleration domain name, with the advanced origin-pull rules configured as shown in the following figure:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/85f7173_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423163955.png)
**Scenario 1**: A client from the Shanghai region accesses `http://www.example.com/vod/`. In this case, the origin-pull request hits the **File directory** rule and is forwarded to `1.1.1.3`.
**Scenario 2**: A client from the Guangdong region accesses `http://www.example.com/`. In this case, the origin-pull request hits both the **Homepage** rule and the **Client IP** rule. As the **Homepage** rule has a higher priority, the origin-pull request is forwarded to `1.1.1.5`.
**Scenario 3**: A client from the Guangdong region accesses `http://www.example.com/image/1.jpg`. In this case, the origin-pull request hits the **File extension**, **Full path**, and **Client IP** rules at the same time. As a path-based rule has a higher priority over an IP-based rule, and the **Full path** rule is listed lower than the **File extension** rule, the origin-pull request is forwarded to `1.1.1.4`.

