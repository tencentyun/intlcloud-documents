This document discusses the best practices of request rate performance optimization on Tencent Cloud COS.

The typical workload capacity provided by Tencent Cloud COS is 1,000 PUT requests per second, or 2,000 GET requests per second. If your workload exceeds the above thresholds, you can follow this guide to expand and optimize the performance of the request rate.

>Request load refers to the number of requests initiated per second, rather than the number of concurrent connections. That is, you can send hundreds of new connection requests within 1 second while maintaining thousands of connections.


Tencent Cloud COS supports performance expansion to provide a higher request rate. In case of a high GET request load, you are recommended to use COS in combination with Tencent Cloud CDN products. See [best practice for using COS with CDN](https://intl.cloud.tencent.com/document/product/436/18424). If the overall request rate of the bucket is expected to exceed 2,000 PUT/LIST/DELETE requests per second, [contact us](<https://intl.cloud.tencent.com/support>) to prepare for the workload and avoid limits on requests.

>If your mixed request load only occasionally reaches 1,200 per second and does not exceed 2,000 per second in bursts, you can ignore this guide.

## Mixed Request Load

When a large number of objects need to be uploaded, the ObjectKey you selected may cause performance problems. Here is a brief description of how Tencent Cloud COS stores object key values.

Tencent Cloud maintains the key values of buckets and objects as indexes in each service region of COS, and the ObjectKeys are stored in the UTF-8 binary order in multiple partitions of the index. Due to such large number of key values, for example, using timestamps or alphabetical order may consume the read/write performance of the partition where the key values are located. Taking the bucket path `testbucket-123454321.cos.ap-beijing.myqcloud.com` as an example, we provide some cases that may consume the index performance:

```
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

If the typical load of your business exceeds 500 requests per second, you should avoid using the sequential key values in the above case. When your business must use characters such as sequential numbers or dates and time as ObjectKeys, you can add random prefixes to key names using certain methods, so as to manage key values in multiple index partitions and improve the performance of centralized load. Here are some methods to add randomness to key values.

**All the following methods are available to improve the access performance of a single bucket. If the typical load of your business exceeds 500 requests per second, you still need to [contact us](<https://intl.cloud.tencent.com/support>) to prepare for your business load in advance while performing the following methods.**

### Add hexadecimal hash prefixes

The most direct way to increase the randomness of the ObjectKey is to add a hash string as a prefix to the front of the key name. For example, when uploading an object, calculate the SHA1 or MD5 hash of the path key value, and add some characters as prefix to the key name. Generally, a hash prefix with a length of 2-4 characters can meet your needs.
<pre>
<font color="red">faf1</font>-20170701/log120000.tar.gz
<font color="red">e073</font>-20170701/log120500.tar.gz
<font color="red">333c</font>-20170701/log121000.tar.gz
<font color="red">2c32</font>-20170701/log121500.tar.gz
</pre>

>Since the key values in Tencent Cloud COS are indexed in the UTF-8 binary order, you may need to initiate 65,536 GET Bucket operations to obtain the original complete 20170701 prefix structure when performing the GET Bucket operation.

### Add enumerated value prefixes

To remain the usability of ObjectKey retrieval, you can enumerate some prefixes based on the types of your files for the grouping of objects. Prefixes with the same enumeration value share the capabilities of the index partition where they are located.

```
logs/20170701/log120000.tar.gz
logs/20170701/log120500.tar.gz
logs/20170701/log121000.tar.gz
...
images/image001/indexpage1.jpg
images/image002/indexpage2.jpg
images/image003/indexpage3.jpg
...
```

If the access load remains as high as more than 500 requests per second under the same enumerated prefix, you can refer to the previous method to add a hash prefix after the enumerated value to implement multiple index partitions, so as to improve the read/write performance.
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

### Reverse the key name string

When your business has to use continuously incremental ID or date, or a large number of successive prefix objects needs to be uploaded at a time, refer to the following typical method:

```
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

The naming method of key values described above easily consumes the performance of index partitions where the key values prefixed with `2017` and `id` are located. In this case, reverse part of the key prefix to allow for a certain randomness.

```
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

## High GET Request Load

If your business load primarily involves GET request (i.e. download request), in addition to complying with the above guidelines, you are recommended to use COS in combination with the Tencent Cloud CDN service.

Tencent Cloud CDN uses edge acceleration nodes across the country and the globe to minimize latency and improve speed when distributing content to users. Hotspot files can be cached using the prefetch feature, thus reducing the number of GET requests returned to the COS origin server. Refer to [best practice for using COS with CDN](https://intl.cloud.tencent.com/document/product/436/18424).

