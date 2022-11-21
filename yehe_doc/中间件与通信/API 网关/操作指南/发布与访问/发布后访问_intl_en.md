## Overview
After a service is published, you can access APIs in it through its subdomain names or the bound custom domain name.

## Directions
A service provides two forms of subdomain names: `http://{your-unique-id}.{region}.apigateway.myqcloud.com` and `http://{service-id}-{your-unique-id}.{region}.apigw.tencentcs.com`. The following uses the former as an example:

After the release, depending on the release environment, the access path of a specific API is like `http://{your-unique-id}.{region}.apigateway.myqcloud.com/release`.

For example, if your user ID is `123456789`, and you have created a service named `register` in the Guangzhou region (`gz`) with a service ID of `service-n904iiau`, added an API with the path of `/user` to it, and published it in the release environment, then when another user or application needs to access the `/user` API, the correct access path should be `http://service-n904iiau-123456789.ap-guangzhou.apigateway.myqcloud.com/release/user`.

>?As international linkages are affected by a variety of issues that cannot be solved by ISPs in the short term, cross-border access through API Gateway may experience packet loss or timeout. If you mainly access businesses outside the Chinese mainland, we recommend you create resources for businesses in and outside the Chinese mainland respectively, so as to avoid congested cross-border IP ranges and gain better business experience.
