
## Configuration Overview

Tencent Cloud CDN supports adding origin-pull request headers:

- It supports carrying the real client IP to the origin server through the `X-Forward-For` header.
- It supports carrying the real client port to the origin server for analysis through the `X-Forward-Port` header.
- It supports adding various custom headers.

## Configuration Guide

### Configuration limitations

- The maximum number of custom request header rules: 10
- Supported rule types: all content, file extension, folder, and file path. Regular matching is currently not supported.
- If there is already header information in the client request, the configured request header will overwrite the original header during origin-pull.
- Rules are executed from bottom to top. Rules at the bottom of the list have higher priority.
- The `Key` of a custom header can contain 1 to 100 characters of digits `0–9`, letters `a–z, A–Z`, and special symbol `-`.
- The `Value` of a custom header can contain 1 to 1000 characters (Chinese characters are not supported).
- Some standard headers do not support customization. For the detailed list, please see below.

### Configuration instructions

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and then click **Manage** on the right of a domain name to enter its configuration page. Select the **Origin-pull Configuration** tab to find the **Origin-pull Request Header Configuration** section. The feature is disabled and not pre-configured by default.
![](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)
You can add origin-pull header rules when the feature is disabled:
![](https://main.qcloudimg.com/raw/e2972a9d697e45b3f081b68ea5e6badb.png)


> !
> 1. The header used to carry the real client IP is `X-Forward-For`, and its value is the `$client_ip` variable by default, which cannot be modified.
> 2. The header used to carry the real client port is `X-Forward-Port`, and its value is the `$remote_port` variable by default, which cannot be modified.

After a rule is added, the overall configuration will be in the disabled state and will not take effect:
![](https://main.qcloudimg.com/raw/10c8061c2e98c8828e3b153c028db86e.png)
You can click **Adjust Priority** to adjust the rule order, and then toggle the switch on to deploy the rule to the CDN nodes across the entire network.
![](https://main.qcloudimg.com/raw/10c8061c2e98c8828e3b153c028db86e.png)

## Configuration Samples

The origin-pull request header configuration of the acceleration domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)

If the accessed resource is `http://cloud.tencent.com/test/test.mp4`, then:
1. The `*` rule will be hit, so the header `X-Forward-For:$client_ip` will be added, and `$client_ip` will be replaced with the real client IP during origin-pull.
2. The `.mp4` file type and `/test` path will be hit, and as rules are executed from bottom to top, the `x-cdn:Tencent` header will be added.

## Notes

The following standard headers currently cannot be added as origin-pull request headers:

<table>
<tbody><tr>
<td>www-authenticate</td>
<td>authorization</td>
<td>proxy-authenticate</td>
<td>proxy-authorization</td>
</tr>
<tr>
<td>age</td>
<td>cache-control</td>
<td>clear-site-data</td>
<td>expires</td>
</tr>
<tr>
<td>pragma</td>
<td>warning</td>
<td>accept-ch</td>
<td>accept-ch-lifetime</td>
</tr>
<tr>
<td>early-data</td>
<td>content-dpr</td>
<td>dpr</td>
<td>device-memory</td>
</tr>
<tr>
<td>save-data</td>
<td>viewport-width</td>
<td>width</td>
<td>last-modified</td>
</tr>
<tr>
<td>etag</td>
<td>if-match</td>
<td>if-none-match</td>
<td>if-modified-since</td>
</tr>
<tr>
<td>if-unmodified-since</td>
<td>vary</td>
<td>connection</td>
<td>keep-alive</td>
</tr>
<tr>
<td>accept</td>
<td>accept-charset</td>
<td>expect</td>
<td>max-forwards</td>
</tr>
<tr>
<td>access-control-allow-origin</td>
<td>access-control-max-age</td>
<td>access-control-allow-headers</td>
<td>access-control-allow-methods</td>
</tr>
<tr>
<td>access-control-expose-headers</td>
<td>access-control-allow-credentials</td>
<td>access-control-request-headers</td>
<td>access-control-request-method</td>
</tr>
<tr>
<td>origin</td>
<td>timing-allow-origin</td>
<td>dnt</td>
<td>tk</td>
</tr>
<tr>
<td>content-disposition</td>
<td>content-length</td>
<td>content-type</td>
<td>content-encoding</td>
</tr>
<tr>
<td>content-language</td>
<td>content-location</td>
<td>forwarded</td>
<td>x-forwarded-host</td>
</tr>
<tr>
<td>x-forwarded-proto</td>
<td>via</td>
<td>from</td>
<td>host</td>
</tr>
<tr>
<td>referer</td>
<td>referer-policy</td>
<td>allow</td>
<td>server</td>
</tr>
<tr>
<td>accept-ranges</td>
<td>range</td>
<td>if-range</td>
<td>content-range</td>
</tr>
<tr>
<td>cross-origin-embedder-policy</td>
<td>cross-origin-opener-policy</td>
<td>cross-origin-resource-policy</td>
<td>content-security-policy</td>
</tr>
<tr>
<td>content-security-policy-report-only</td>
<td>expect-ct</td>
<td>feature-policy</td>
<td>strict-transport-security</td>
</tr>
<tr>
<td>upgrade-insecure-requests</td>
<td>x-content-type-options</td>
<td>x-download-options</td>
<td>x-frame-options(xfo)</td>
</tr>
<tr>
<td>x-permitted-cross-domain-policies</td>
<td>x-powered-by</td>
<td>x-xss-protection</td>
<td>public-key-pins</td>
</tr>
<tr>
<td>public-key-pins-report-only</td>
<td>sec-fetch-site</td>
<td>sec-fetch-mode</td>
<td>sec-fetch-user</td>
</tr>
<tr>
<td>sec-fetch-dest</td>
<td>last-event-id</td>
<td>nel</td>
<td>ping-from</td>
</tr>
<tr>
<td>ping-to</td>
<td>report-to</td>
<td>transfer-encoding</td>
<td>te</td>
</tr>
<tr>
<td>trailer</td>
<td>sec-websocket-key</td>
<td>sec-websocket-extensions</td>
<td>sec-websocket-accept</td>
</tr>
<tr>
<td>sec-websocket-protocol</td>
<td>sec-websocket-version</td>
<td>accept-push-policy</td>
<td>accept-signature</td>
</tr>
<tr>
<td>alt-svc</td>
<td>date</td>
<td>large-allocation</td>
<td>link</td>
</tr>
<tr>
<td>push-policy</td>
<td>retry-after</td>
<td>signature</td>
<td>signed-headers</td>
</tr>
<tr>
<td>server-timing</td>
<td>service-worker-allowed</td>
<td>sourcemap</td>
<td>upgrade</td>
</tr>
<tr>
<td>x-dns-prefetch-control</td>
<td>x-firefox-spdy</td>
<td>x-pingback</td>
<td>x-requested-with</td>
</tr>
<tr>
<td>x-robots-tag</td>
<td>x-ua-compatible</td>
<td>max-age</td>
<td></td>
</tr>
</tbody></table>
