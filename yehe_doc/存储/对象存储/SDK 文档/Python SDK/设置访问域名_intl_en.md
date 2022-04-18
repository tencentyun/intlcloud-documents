## Overview

This document provides SDK code samples to show how to use the Python SDK to set an access domain.

### Access via the default COS domain

If you use the COS default domain to access COS, the SDK will access COS using a domain name formatted as **{bucket-appid}.cos.{region}.myqcloud.com**.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)
```

### Access via the COS global acceleration domain

If you use the COS global acceleration domain to access COS, the SDK will access COS using a domain name formatted as `{bucket-appid}.cos.accelerate.myqcloud.com`. `region` will not appear in the domain name.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # “region” does not need to be specified if you initialize with “Endpoint”.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

endpoint = 'cos.accelerate.myqcloud.com' # Replace it with your endpoint or the COS global acceleration domain. To use a global acceleration domain, you need to enable the global acceleration feature for the bucket first (see https://intl.cloud.tencent.com/document/product/436/33406).
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Endpoint=endpoint, Scheme=scheme)
client = CosS3Client(config)
```

### Access via a custom COS domain

If you use a custom domain to access COS, the SDK will directly access COS using the **user domain** configured. Neither `bucket` nor `region` will appear in the domain name.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # “region” does not need to be specified if you initialize with a custom domain.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

domain = 'user-define.example.com' # Your custom domain. You need to enable the custom domain for the bucket first (see https://intl.cloud.tencent.com/document/product/436/31507).
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Domain=domain, Scheme=scheme)
client = CosS3Client(config)
```

### Access via the default CDN domain

If you use the CDN default domain to access COS, the SDK will access **CDN** using a domain formatted as **{bucket-appid}.file.mycloud.com** and then access COS via the CDN origin server.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # “region” does not need to be specified if you initialize with “Endpoint”.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

endpoint = 'file.mycloud.com' # Replace it with your default CDN acceleration domain name. For details about how to enable CDN acceleration, visit https://intl.cloud.tencent.com/document/product/436/18670.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Endpoint=endpoint, Scheme=scheme)
client = CosS3Client(config)
```

### Access via a custom CDN domain

If you use a CDN custom domain to access COS, the SDK will directly access **CDN** using the **user domain** configured (neither `bucket` nor `region` will appear in the domain name) and then access COS via CDN origin server.

#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = None              # “region” does not need to be specified if you initialize with a custom domain.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

domain = 'user-define.example-cdn.com' # Your CDN custom domain. You need to enable the CDN custom domain acceleration first (see https://intl.cloud.tencent.com/document/product/436/18670).
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Domain=domain, Scheme=scheme)
client = CosS3Client(config)
```
