

Tencent Cloud Content Delivery Network offers refined origin-pull configurations to forward origin-pull requests based on path (i.e., specifying a file type, folder, full-path file, or homepage for origin-pull) and client IP region.

>! Origin-pull based on client IP region is in beta, please stay tuned for the official launch.

## Configuration Guide

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **Basic Configuration** tab to find the **Advanced Origin-pull Configuration** section.

![](https://main.qcloudimg.com/raw/17e0385a7cea2cbdd0ae012cae8b2555.png)

### Adding rules

You can click **Add Rule** to add rules as needed.
![](https://main.qcloudimg.com/raw/ef2ae0e51a0cb032d493f89b8029b316.png)

**Limitations**

- Each domain name can be configured with up to 50 rules.
- The origin-pull address of a single rule can be an IP, domain name, and port (range: 0 - 65535; port can be omitted). If "HTTPS" or "Follow Protocol" is selected as the origin-pull protocol, the port should be 443 or left empty.
- More actions: you can adjust rule priority and edit or delete multiple rules in batches.

>?
>- In the rule list, a lower rule has the higher priority. Note that if you rearrange a rule in the list, only the priority of rules of the same type are affected.
>- If a request matches both rule types, rules will be executed in the order of path-based rules and then the client IP region-based rules.
For example, when there are two origin-pull rules: "forwarding all requests from Jiangsu province to `1.1.1.1`" and "forwarding the requests accessing `/test` to `2.2.2.2`", then if a request from Jiangsu wants to access the directory `/test`, the request will be forwarded to `2.2.2.2`.
