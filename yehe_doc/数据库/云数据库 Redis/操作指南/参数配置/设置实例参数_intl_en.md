This document describes how to configure instance parameters in the TencentDB for Redis console.

## Overview
Some of the parameters of TencentDB for Redis instances can be customized. In the [console](https://console.cloud.tencent.com/redis), you can view and modify these parameters and view their modification history.

>?To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** page.

## Modifying Parameters
### [Modifying one parameter](id:xgdgcs)
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Parameter Settings** tab, locate the desired parameter in the parameter list and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column.
![](https://main.qcloudimg.com/raw/1c715f076679b7aa7405b7dc35e744f5.png)
3. Modify the value within the restrictions stated in the **Acceptable Values** column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the modification. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
![](https://main.qcloudimg.com/raw/b3cd3751c3b57a4e2fa5bee19dd82198.png)

### Modifying parameters in batches
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Parameter Settings** tab and click **Modify Current Value**.
![](https://main.qcloudimg.com/raw/c9dcf38d03f68dae0b8b56b291c14f98.png)
3. Locate the desired parameters and modify their values in the **Current Value** column. After confirming that everything is correct, click **OK**.
![](https://main.qcloudimg.com/raw/e078a0b0108606456b2e569084ccab5e.png)

### Importing from template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Parameter Settings** tab and click **Import from Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/dec98b7c42cef6671890812602fc5ce5.png)
For more information on import from template, see [Applying Parameter Templates](https://intl.cloud.tencent.com/document/product/239/41810).

## Viewing Parameter Modification Logs
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. View the parameter modification history on the **Parameter Settings** > **Modification Log** tab.
![](https://main.qcloudimg.com/raw/91089fb8d13721731d18a804fcaded3a.png)

## Supported Custom Parameters
<table>
<tr><th>Parameter</th><th>Description</th><th>Supported Version</th></tr>
<tr>
<td>disable-command-list</td>
<td>Disable commands that have high time complexity or are highly risky. The disabled commands will not be allowed to run in this instance. To disable multiple commands, separate them with commas, such as `flushdb,keys`.</td>
<td>Redis 2.8, 4.0, and 5.0</td>
<tr>
<td>maxmemory-policy</td>
<td>Select one of the following eviction policies used to evict data when the Redis in-memory cache was used up.
<li>volatile-lru: Evict keys that have an `expire` set by trying to remove the less recently used (LRU) keys first.
<li>allkeys-lru: Evict keys by trying to remove the less recently used (LRU) keys first.
<li>volatile-random: Randomly evict keys with an expire set.
<li>allkeys-random: Randomly evict keys.
<li>volatile-ttl: Evict keys with an expire set, and try to evict keys with a shorter time to live (TTL) first.
<li>noeviction: Do not evict keys but return errors when the memory limit was reached.
<br>LRU and TTL are implemented by randomized and approximation algorithms.	</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>cluster-node-timeout</td>
<td>Set the timeout threshold for a cluster node. If a cluster node remains unreachable longer than the threshold, it will be deemed as a failed node.</td>
<td>Redis 4.0 and 5.0</td></tr>
<tr>
<td>hash-max-ziplist-entries</td>
<td>Hashes that meet both of the following conditions will be encoded as ziplist.
<li>The biggest hash entry is smaller than the value (in bytes) of `hash-max-ziplist-value`.
<li>The number of hash entries is smaller than the value of `hash-max-ziplist-entries`.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>hash-max-ziplist-value</td>
<td>Hashes that meet both of the following conditions will be encoded as ziplist.
<li>The biggest hash entry is smaller than the value (in bytes) of `hash-max-ziplist-value`.
<li>The number of hash entries is smaller than the value of `hash-max-ziplist-entries`.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>proxy-slowlog-log-slower-than</td>
<td>Set the proxy slow log threshold (in milliseconds). In the proxy, queries that are executed longer than the threshold will be logged.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>set-max-intset-entries</td>
<td>Sets that meet both of the following conditions will be encoded as intset.
<li>All set members are composed of just strings.
<li>All set members can be interpreted as base-10 integers within the range of 64-bit signed integers.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>slowlog-log-slower-than</td>
<td>Set the slow log threshold (in milliseconds). Queries that are executed longer than the threshold will be logged.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>timeout</td>
<td>Set the timeout threshold (in seconds) for connections. Client connections that remain idle longer than the threshold will be closed.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>zset-max-ziplist-entries</td>
<td>Sorted sets that meet both of the following conditions will be encoded as ziplist.
<li>The biggest sorted set element is smaller than the value (in bytes) of `zset-max-ziplist-value`.
<li>The number of sorted set elements is smaller than the value of `zset-max-ziplist-entries`.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>zset-max-ziplist-value</td>
<td>Sorted sets that meet both of the following conditions will be encoded as ziplist.
<li>The biggest sorted set element is smaller than the value (in bytes) of `zset-max-ziplist-value`.
<li>The number of sorted set elements is smaller than the value of `zset-max-ziplist-entries`.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>notify-keyspace-events</td>
<td>Specify the type of notifications sent by the server. The value of this parameter is composed of multiple characters listed as follows:
<li>Character: Notification type
<li>K: Keyspace events, published with `__keyspace@&lt;db>__` prefix.
<li>E: Keyevent events, published with `__keyevent@&lt;db>__` prefix.
<li>g: Generic commands (non-type specific) like DEL, EXPIRE, RENAME, etc.
<li>$: String commands
<li>l: List commands
<li>s: Set commands
<li>h: Hash commands
<li>z: Sorted set commands
<li>x: Expired events (events generated every time a key expires)
<li>e: Evicted events (events generated when a key is evicted for maxmemory)
<li>A: Alias for `g$lshzxe`
<br>Enabling keyspace event notifications consumes CPU resources, so this type of notification is disabled by default. To configure the server to send notifications, the parameter value must include `K` or `E`. For example, to subscribe to evicted event notifications of the keyevent events, set the parameter to `Ee`; to subscribe to all types of notifications, set the parameter to `AKE`.</td>
<td>Redis 2.8, 4.0, and 5.0</td></tr>
<tr>
<td>list-max-ziplist-entries</td>
<td>Lists that meet both of the following conditions will be encoded as ziplist.
<li>The biggest list element is smaller than the value (in bytes) of `list-max-ziplist-value`.
<li>The number of list elements is smaller than the value of `list-max-ziplist-entries`.</td>
<td>Redis 2.8</td></tr>
<tr>
<td>list-max-ziplist-value</td>
<td>Lists that meet both of the following conditions will be encoded as ziplist.
<li>The biggest list element is smaller than the value (in bytes) of `list-max-ziplist-value`.
<li>The number of list elements is smaller than the value of `list-max-ziplist-entries`.</td>
<td>Redis 2.8</td></tr>
</table>


