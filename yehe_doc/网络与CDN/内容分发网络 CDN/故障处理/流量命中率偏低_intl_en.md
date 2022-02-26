## Error Description

The real-time traffic hit rate is well below your expectation.

## Possible Reasons

- The cache is purged.
  Cache purge will clear the specified content on the node, leading to a temporarily low traffic hit rate.
- There are new contents on the origin server.
  Large numbers of new contents will cause origin-pulls by CDN nodes, resulting in a low traffic hit rate.
- There are exceptions on the origin server.
  - If it is malfunctioning with multiple 4XX or 5XX errors, the traffic hit rate will be affected.
- The caching policy is not configured properly.
  You should configure it based on your business needs.
- Range GETs is disabled.
  In this case, files will be pulled in their entirety instead of multiple parts as requested during origin-pull, which increases the origin-pull traffic and lowers the hit rate.
- The requests hit the **Ignore all** cache key rule configured for the domain name while the origin server is set to return different contents according to the parameters.
  In this case, all contents will be cached and a specific content requested by the corresponding parameter cannot be matched, thus lowering the traffic hit rate.

## Solutions

1. Check to ensure your origin server works properly.
2. It is normal to see a decrease in traffic hit rate when you purge the cache or have new contents on the origin server.
3. Do not set the origin server to return different resources according to URL parameters if the **Ignore all** cache key rule is used.
4. Set the caching rule based on your business needs.

## Troubleshooting Procedure
[](id:step1)
Step 1. Check whether your origin server is exceptional or the cache is purged.
   - If it is, the hit rate will be low.
   - If it is not, go to [Step 2](#step2).
[](id:step2)
Step 2. Check whether your origin server returns different contents according to URL parameters.
   - If it does, go to [Step 3](#step3).
   - If it does not, go to [Step 5](#step5).
[](id:step3)
Step 3. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Cache Configuration** tab to find the **Cache Key Rule Configuration** section. Then check whether the **Ignore parameter** is configured as **Not ignore**.

   - If it is not, go to [Step 4](#step4).
   - If it is, go to [Step 5](#step5).
[](id:step4)
Step 4. Click **Modify** on the right of the rule, tick **Not ignore**, and click **Save**.

>? If this operation is not suitable for your business, you can use the **Reserve Specified Parameter** feature as needed. For more information, please see [Cache Key Rule Configuration](https://intl.cloud.tencent.com/document/product/228/35316).
>
[](id:step5)
Step 5. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Cache Configuration** tab to find the **Node Cache Validity Configuration** section and check whether the caching rules configured comply with your business needs.
   - If it does, perform [Step 5](#step5).
   - If it does not, consult [Node Caching Rule Configuration](https://intl.cloud.tencent.com/document/product/228/38424) and set the rules as needed.
