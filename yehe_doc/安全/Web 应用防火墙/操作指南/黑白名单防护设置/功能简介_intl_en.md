The blocklist/allowlist feature of WAF allows you to add access source IPs that pass WAF-protected domains to the blocklist or allowlist and add multiple HTTP sections to the precise allowlist. Key features include IP blocklist/allowlist settings and precise allowlist settings.
- IP blocklist/allowlist setting: You can set domain name-specific, IP range-specific, or global IP blocklist/allowlist rules.
- Precise allowlist setting: You can add the access requests from specified public network users to the allowlist by combining and matching HTTP message sections such as request path, GET parameters, POST parameters, `Referer`, and `User-Agent`.

Meanwhile, you can add a domain name-specific or global blocklist/allowlist which will take effect in the following priority order:
- The priority of the blocklist/allowlist is only lower than that of the custom precise allowlist, but higher than that of other detection logic.
- The priority of blocklist/allowlist settings is in descending order: precise allowlist > global allowlist > domain name-specific allowlist > domain name-specific blocklist > global blocklist > other WAF module logic.
