## Error Description

After the node cache expiration time is set and prefetch is completed, the request still cannot hit the node cache.

## Cause

1. There are multiple cache rules, but their priorities are unclear.
2. "Follow origin server" is configured, but the `Cache-Control` field on the origin server is set to `no-cache/no-store/private`.

## Solution

1. Set the cache rule priority correctly.
   You can set multiple CDN cache rules. The lower the rule position, the higher the rule priority. You need to ensure that the rule priority meets your expectation for the rules to take effect as expected.
2. Set the cache validity correctly.
Check whether the cache validity set in the console is too short.
>! URLs with infrequent file access have the risk of being removed from the node cache even they meet all cache rules.
3. Check whether the cache rules meet your expectation.
	- Check whether the "Ignore Query String" setting in a CDN cache key rule causes a failure to cache the resources on the node.
	- Check whether "No cache" is set in a CDN node cache validity rule.
	- Check whether the header of the request from the origin server returns `no-cache/no-store/private` during origin-pull when the set CDN node cache expiration time is the same as that on the origin server.

## Troubleshooting Procedure

1. Check the cache rule priority (the one at the bottom has the highest priority).
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, locate the desired domain name, click **Manage** in the **Operation** column to enter the **Domain Configuration** page, switch to the **Cache Configuration** tab, and you can find the **Cache Key Rule Configuration**. As shown below, the priority of the rule where .jpg files are excluded for "Ignore Query String" is higher than that of the rule where "Ignore Query String" is configured for all files. You need to ensure that the business cache policies meet the priority settings.

2. Check the cache validity.
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, locate the desired domain name, and click **Manage** > **Cache Configuration** > **Node Cache Validity Configuration**. As shown below, if the set cache validity is too short, the cache configuration may be mistaken as ineffective. Ensure that the cache configuration meets your business cache policies.

3. Check the cache policies.
Check whether the policies in the cache key rule configuration and node cache validity configuration meet the expectation.
If "Follow origin server" is configured, ensure that the `Cache-Control` field on the origin server is not set to `no-cache/no-store/private`.
4. Prefetch the resource to be cached again. After prefetch is completed, request the resource again.

