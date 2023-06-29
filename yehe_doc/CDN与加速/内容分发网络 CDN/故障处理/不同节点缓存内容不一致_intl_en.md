## Error Description

Users in different regions receive different contents for the same resource URL.

## Possible Reasons

- Reason 1: The cache key is configured to **Filter All** for the domain name, and the origin server is set to return different resources according to the parameters.
  In this case, different nodes may cache different contents due to the different parameters of their first-received access requests. When the same request accesses a different node, the returned contents will be different. 

- Reason 2: The requested resource is not purged after being updated on the origin server.
  CDN caches resources based on the URL. If the content on the origin server is updated but the URL is not changed, when a user sends a request to the URL, the content cached on the node previously will be returned. Also, the access frequency varies by region, so the resource cache validity may be different in each region. When a user request accesses a cache node, if the requested resource on the node is expired, the request will be forwarded to the origin server, and the latest content is pulled and returned. Some nodes have the latest content, and some have the legacy content.  

## Solutions

1. Do not set the origin server to return different resources according to URL parameters if the "Filter All" cache key is used.
2. Purge the URL resource after it is updated on the origin server.

## Troubleshooting Procedure

Step 1. Check whether your origin server returns different resources according to URL parameters.
   - If it does, please go to [Step 2](##step2).
   - If it does not, please go to [Step 4](#step4).

[](id:step2)
Step 2. Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page. Open the **Cache Configuration** tab to find the **Cache Key Configuration** section, and check whether the **Ignore Query String** is configured as **Not Filter**.

   - If it is not, please go to [Step 3](##step3).
   - If it is, please go to [Step 4](#step4).



[](id:step3)
Step 3. Click **Modify** on the right of the rule, tick **Not Filter**, and click **Save**.

> ?If this operation is not suitable for your business, you can use the **Reserve Specified Parameter** feature as needed. For more information, please see [Cache Key Configuration](https://intl.cloud.tencent.com/document/product/228/35316).

[](id:step4)
Step 4. Click **Purge and Prefetch** on the left sidebar to purge the resource that is updated on the origin server.

> ?You can also bind the API for resource purge, so that resources can be purged across the entire network immediately once updated, guaranteeing the content consistency for access. For more information, please see [PurgeUrlsCache](https://intl.cloud.tencent.com/document/product/228/33601) and [PurgePathCache](https://intl.cloud.tencent.com/document/product/228/33602).
