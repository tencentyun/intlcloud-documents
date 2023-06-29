## Configuration Overview

Tencent Cloud CDN supports adding origin-pull request headers:

- Carries the real client IP to the origin server through the `X-Forward-For` header.
- Carries the real client port to the origin server for analysis through the `X-Forward-Port` header.
- Adds custom headers.

You can also set and delete custom origin-pull request headers.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and then click **Manage** on the right of a domain name to enter its configuration page. Select the **Origin-pull Configuration** tab to find the **Origin-pull Request Header Configuration** section. The feature is disabled and not pre-configured by default.
![img](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)

### Operation

| Operation | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Set     | Sets the value of a specified request header parameter.<br/>If the target header does not exist, a new one will be added.<br/>If the origin-pull request header parameter already exists, the new request header will overwrite the old one as duplicate headers are not allowed.|
| Add     | Adds a specified origin-pull request header parameter.<br/>If the target header already exists, the new request header will overwrite the old one as duplicate headers are not allowed.|
| Delete     | Deletes a specified request header parameter.                                       |

>!
> - Rules are executed from bottom to top, and the priority is meaningful for the same type of operations only, that is, the priorities of multiple "Set", "Add", and "Delete" rules are independent.
> - If an origin-pull request header parameter is configured with multiple rules of different operations, the operations will be conducted in the order of "Add", "Delete", and "Set". For example, if the header `X-CDN` is configured with rules of "Add", "Delete", and "Set", it will be added, then deleted, and finally set.

### Header parameter

| Header Parameter       | Description                                                         |
| -------------- | ------------------------------------------------------------ |
| X-Forward-For  | The header used to carry the real client IP. Its value defaults to `$client_ip` variable, which cannot be modified. |
| X-Forward-Port | The header used to carry the real client port. Its value defaults to `$remote_port` variable, which cannot be modified. |
| Custom header     | Key: 1 to 100 characters, including digits (0 - 9), lowercase letters (a - z), uppercase letters (A - Z), and hyphens (-).<br>Value: 1 to 1000 characters. Chinese characters are not supported.<br>Some standard headers cannot be set, added, or deleted by the user. For the detailed list, please see [Notes](#notice). |

> !
> - Up to 10 origin-pull request header rules can be configured.
> - Supported rule types: all content, specified file type, specified folder, and specified file. Regex match is currently not supported.



## Configuration Samples

The origin-pull request header configuration of the acceleration domain name `cloud.tencent.com` is as follows:
![img](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
If the accessed resource is `http://cloud.tencent.com/test/test.mp4`, then:

1. It hits the `*` rule, so the header `X-Forward-For:$client_ip` will be added, and `$client_ip` will be replaced with the real client IP during origin-pull.
2. It hits both the `.mp4` file type tule and `/test` path rule. The two rules are of the same type, "Add". As the lower rule has the higher priority, the header `x-cdn:Tencent` is added.

<span id="notice"></span>

## Notes
In origin-pull request header rules, the following standard headers currently cannot be set, added, or deleted:

| www-authenticate              | authorization                    | proxy-authenticate             | proxy-authorization                 |
| ----------------------------- | -------------------------------- | ------------------------------ | ----------------------------------- |
| age                           | cache-control                    | clear-site-data                | expires                             |
| pragma                        | warning                          | accept-ch                      | accept-ch-lifetime                  |
| early-data                    | content-dpr                      | dpr                            | device-memory                       |
| save-data                     | viewport-width                   | width                          | last-modified                       |
| etag                          | if-match                         | if-none-match                  | if-modified-since                   |
| if-unmodified-since           | vary                             | connection                     | keep-alive                          |
| accept                        | accept-charset                   | expect                         | max-forwards                        |
| access-control-allow-origin   | access-control-max-age           | access-control-allow-headers   | access-control-allow-methods        |
| access-control-expose-headers | access-control-allow-credentials | access-control-request-headers | access-control-request-method       |
| origin                        | timing-allow-origin              | dnt                            | tk                                  |
| content-disposition           | content-length                   | content-type                   | content-encoding                    |
| content-language              | content-location                 | forwarded                      | x-forwarded-host                    |
| x-forwarded-proto             | via                              | from                           | host                                |
| referer-policy                | allow                            | server                         | accept-ranges                       |
| range                         | if-range                         | content-range                  | cross-origin-embedder-policy        |
| cross-origin-opener-policy    | cross-origin-resource-policy     | content-security-policy        | content-security-policy-report-only |
| expect-ct                     | feature-policy                   | strict-transport-security      | upgrade-insecure-requests           |
| x-content-type-options        | x-download-options               | x-frame-options(xfo)           | x-permitted-cross-domain-policies   |
| x-powered-by                  | x-xss-protection                 | public-key-pins                | public-key-pins-report-only         |
| sec-fetch-site                | sec-fetch-mode                   | sec-fetch-user                 | sec-fetch-dest                      |
| last-event-id                 | nel                              | ping-from                      | ping-to                             |
| report-to                     | transfer-encoding                | te                             | trailer                             |
| sec-websocket-key             | sec-websocket-extensions         | sec-websocket-accept           | sec-websocket-protocol              |
| sec-websocket-version         | accept-push-policy               | accept-signature               | alt-svc                             |
| date                          | large-allocation                 | link                           | push-policy                         |
| retry-after                   | signature                        | signed-headers                 | server-timing                       |
| service-worker-allowed        | sourcemap                        | upgrade                        | x-dns-prefetch-control              |
| x-firefox-spdy                | x-pingback                       | x-requested-with               | x-robots-tag                        |
| x-ua-compatible               | max-age                          |                                |                                     |
