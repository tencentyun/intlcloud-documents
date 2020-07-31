## Overview
This document discusses best practices for request rate performance optimization on Tencent Cloud COS.

Tencent Cloud COS supports a typical workload capacity of 30,000 PUT requests per second or 30,000 GET requests per second. If your workload exceeds the above thresholds, you can follow this guide to expand and optimize your request rate performance.

>The request load refers to the number of requests initiated per second rather than the number of concurrent connections. That is, you can send hundreds of new connection requests per second while maintaining thousands of existing connections without issue.


Tencent Cloud COS supports performance expansion to provide a higher request rate. In the case of a high GET request load, we recommend using COS in combination with Tencent Cloud CDN products. For more information, see [Domain Name Management](https://intl.cloud.tencent.com/document/product/436/18424). If the overall request rate of the bucket is expected to exceed 30,000 PUT/LIST/DELETE requests per second, [contact us](https://intl.cloud.tencent.com/support) to prepare for the workload and avoid request limits.

>If you have a mixed request load that only occasionally reaches 30,000 per second and does not exceed 30,000 per second during bursts, you can ignore this guide.

## Directions
### Mixed request load

When a large number of objects need to be uploaded, the ObjectKey you select may cause performance issues. Below is a brief description of how Tencent Cloud COS stores object key values.

Tencent Cloud maintains bucket and object key values as indexes in each service region of COS; ObjectKeys are stored in UTF-8 binary order in the partitions of the index. Due to such a large number of key values, using timestamps or alphabetical order, for example, may consume the read/write performance capacity of the partition where the key values are located. Taking the bucket path `examplebucket-1250000000.cos.ap-beijing.myqcloud.com` as an example, below are some cases that may consume index performance capacity:

```bash
20170701/log120000.tar.gz
20170701/log120500.tar.gz
20170701/log121000.tar.gz
20170701/log121500.tar.gz
...
image001/indexpage1.jpg
image002/indexpage2.jpg
image003/indexpage3.jpg
...
```

If your typical workload exceeds 30,000 requests per second, you should avoid using sequential key values as shown in the above case. When you need to use characters such as sequential numbers, dates, or time values as ObjectKeys, you can add random prefixes to key names, so as to manage key values in multiple index partitions and improve centralized load performance. Below are some methods for adding a random element to key values.

>The following methods can all be used to improve the access performance of a single bucket. If the typical load of your business exceeds 30,000 requests per second, you still need to [contact us](https://intl.cloud.tencent.com/support) to prepare for your business load in advance even while performing the following methods.**

#### Adding hexadecimal hash prefixes

The most direct way to increase ObjectKey randomness is to add a hash string prefix at the very front of the key name. For example, when uploading an object, calculate the SHA1 or MD5 hash of the path key value and add a few characters as a prefix to the key name. Generally, a hash prefix with a length of 2-4 characters will suffice.
<pre>
<font color="red">faf1</font>-20170701/log120000.tar.gz
<font color="red">e073</font>-20170701/log120500.tar.gz
<font color="red">333c</font>-20170701/log121000.tar.gz
<font color="red">2c32</font>-20170701/log121500.tar.gz
</pre>

>Since the key values in Tencent Cloud COS are indexed in UTF-8 binary order, you may need to initiate 65,536 GET Bucket operations to obtain the original complete 20170701 prefix structure.

#### Adding enumerated value prefixes

If you still want to make sure your ObjectKeys are easily retrievable, you can enumerate prefixes based on file type to help group your objects. Prefixes with the same enumeration value share the capabilities of the index partition where they are located.

```bash
logs/20170701/log120000.tar.gz
logs/20170701/log120500.tar.gz
logs/20170701/log121000.tar.gz
...
images/image001/indexpage1.jpg
images/image002/indexpage2.jpg
images/image003/indexpage3.jpg
...
```

If the access load for an enumerated prefix remains at more than 30,000 requests per second, you can refer to the previous method to add a hash prefix after the enumerated value to implement multiple index partitions, so as to improve the read/write performance.
<pre>
logs/<font color="red">faf1</font>-20170701/log120000.tar.gz
logs/<font color="red">e073</font>-20170701/log120500.tar.gz
logs/<font color="red">333c</font>-20170701/log121000.tar.gz
...
images/<font color="red">0165</font>-image001/indexpage1.jpg
images/<font color="red">a349</font>-image002/indexpage2.jpg
images/<font color="red">ac00</font>-image003/indexpage3.jpg
...
</pre>

#### Reversing the key name string

When you need to use incremental IDs or dates or need to upload a large number of objects with successive prefixes in a single upload, refer to the following method:

```shell
20170701/log0701A.tar.gz
20170701/log0701B.tar.gz
20170702/log0702A.tar.gz
20170702/log0702B.tar.gz
...
id16777216/album/hongkong/img20170701121314.jpg
id16777216/music/artist/tony/anythinggoes.mp3
id16777217/video/record20170701121314.mov
id16777218/live/show/date/20170701121314.mp4
...
```

The naming method for key values shown above easily consumes the performance capacity of index partitions where the key values prefixed with `2017` and `id` are located. In this case, reverse part of the key prefix to allow for a certain element of randomness.

```bash
10707102/log0701A.tar.gz
10707102/log0701B.tar.gz
20707102/log0702A.tar.gz
20707102/log0702B.tar.gz
...
61277761di/album/hongkong/img20170701121314.jpg
61277761di/music/artist/tony/anythinggoes.mp3
71277761di/video/record20170701121314.mov
81277761di/live/show/date/20170701121314.mp4
...
```

### High GET request load

If your workload primarily involves GET requests (i.e. download requests), in addition to complying with the above guidelines, we recommend using COS in combination with Tencent Cloud CDN services.

Tencent Cloud CDN has edge acceleration nodes all across China and around the globe that can be used to minimize latency and improve speed when distributing content to users. Hot files can be cached using the prefetch feature, thus reducing the number of GET requests returned to the COS origin server. For more information, see [Domain Name Management](https://intl.cloud.tencent.com/document/product/436/18424).
