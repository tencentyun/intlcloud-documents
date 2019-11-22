

Cloud Object Storages (COS) is a distributed storage service provided by Tencent Cloud to store massive files. You can store and view data at any time over the network. Tencent Cloud COS provides scalable, affordable, reliable and secure data storage services for all users.

You can gain the access to COS easily via console, API, SDK, tools, among other diverse ways, to store and manage massive data. COS allows you to upload, download and manage files in different formats using its user-friendly Web interface. The CDN nodes distributed nationwide can accelerate your file download.

## Storage Type

COS is available in three classes depending on the access frequency: Standard, Standard_IA, and Archive Storage.

>Default is Standard.

#### Standard

**Use Cases:** Hotspot videos, social images, mobile Apps, game programs, and dynamic websites.

- COS Standard is an object storage service with high reliability, availability, and performance.
- Its low latency and high throughput make it well suitable for the use cases involving lots of hotspot files or frequent data access.



#### Standard_IA

**Use Cases:** Network disk data, big data analysis, government and enterprise business data, infrequently-accessed archives, and monitoring data.
- COS Infrequent Access is a reliable object storage service with low storage cost and low access latency.
- COS Infrequent Access is provided at a low storage cost, and enables you to access the first byte in milliseconds. You can retrieve the data quickly without waiting. The data retrieval is chargeable, so this storage class is suitable for the use cases involving infrequent access.



#### Archive Storage

**Use Cases:** Archive data, medical images, scientific data, and film and video materials.

- Archive Storage is a highly reliable object storage service that has ultra-low storage cost and long-term data retention.
- Featuring the lowest storage price, Archive Storage needs a longer time to read data and is suitable for archived data that needs to be stored for a long time.



#### Comparison

| Item                     | Standard                         | Standard_IA         | Archive                                                  |
| ------------------------ | -------------------------------- | ------------------- | -------------------------------------------------------- |
| Data persistence         | 99.999999999%                    | 99.999999999%       | 99.999999999%                                            |
| Service availability     | 99.95%                           | 99.9%               | 99.9%                                                    |
| Response                 | Within milliseconds              | Within milliseconds | Prior application for data restoration required          |
| Minimum object size      | Calculated by actual object size | 64 KB               | 64 KB                                                    |
| Minimum billing duration | No limit                         | 30 days             | 90 days                                                  |
| Supported regions        | All                              | All                 | Public cloud regions only                                |
| Storage cost             | Standard                         | Low                 | Very low                                                 |
| Data retrieval cost      | None                             | Low                 | High                                                     |
| Read/write request cost  | Very low                         | Low                 | Very low (data needs to be restored to standard storage) |

## Related Documents
See the following documents for information on the regions, features and specifications supported by Tencent Cloud COS.
- [Regions & Endpoints](http://intl.cloud.tencent.com/document/product/436/6224)
- [Features](http://intl.cloud.tencent.com/document/product/436/8186)
- [Specifications and Use Limits](http://intl.cloud.tencent.com/document/product/436/14518)

See the following documents to learn about the basic elements of Tencent Cloud COS: buckets and objects.
- [Bucket Overview](http://intl.cloud.tencent.com/document/product/436/13312)
- [Object Overview](http://intl.cloud.tencent.com/document/product/436/13324)

