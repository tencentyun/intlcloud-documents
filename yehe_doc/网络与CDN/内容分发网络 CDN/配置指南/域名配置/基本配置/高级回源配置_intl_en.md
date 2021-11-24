

Tencent Cloud CDN allows you to configure fine-grained origin-pull based on origin-pull rules, such as path-based rules (i.e., specifying a file type, folder, full file path, or homepage for origin-pull) and client IP region-based rules.

>!
>- Origin-pull based on client IP region is in beta. Please stay tuned for the official launch.
>- Only primary origin servers support advanced origin-pull. This configuration will inherit the origin type and origin domain settings of the primary origin server, regardless of different types of rules.

## Directions

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **Basic Configuration** tab to find the **Advanced Origin-pull Configuration** section.
![](https://main.qcloudimg.com/raw/17e0385a7cea2cbdd0ae012cae8b2555.png)

### Adding rules

Add rules for advanced origin-pull as needed. To add one, click **Edit** in the **Primary Origin** section and then **Advanced Origin-pull Configuration**.
![](https://main.qcloudimg.com/raw/ef2ae0e51a0cb032d493f89b8029b316.png)

**Configuration limitations**

- Each domain name can be configured with up to 50 rules.
- The origin-pull address of a single rule can be an IP, domain name, and port (range: 0 - 65535; port can be omitted). If "HTTPS" or "Follow Protocol" is selected as the origin-pull protocol, the port should be 443 or left empty.
- More actions: you can adjust rule priority and edit or delete multiple rules in batches.

>?
>- Rules at the bottom of the list have higher priority. The priority is meaningful for the same type of origin-pull rules only, that is, the priority of path-based rules (i.e., specifying a file type, folder, full-path file, or homepage for origin-pull) and the priority of client IP region-based rules are independent.
>- If a request matches both rule types, rules will be executed in the order of path-based rules and then the client IP region-based rules.
For example, there are two origin-pull rules: "forwarding the requests initiated by any IP address of Jiangsu to `1.1.1.1`" and "forwarding the requests accessing `/test` to `2.2.2.2`". If a Jiangsu-located IP accesses the directory `/test`, the request will be forwarded to `2.2.2.2`.
