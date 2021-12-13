## Overview

TDMQ for Pulsar 2.7.1 and above clusters already support Apache Pulsar SDK for Python. This document describes how to access the SDK.

## Prerequisites

- Get the access address
  Copy the access address on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the TDMQ for Pulsar console.

- Get the token
  Configure the role and permission as instructed in [Role and Authentication](https://intl.cloud.tencent.com/document/product/1110/42936) and get the token of the role.

## Directions

1. Install the Python client in your client environment as instructed in [Pulsar Python client](http://pulsar.apache.org/docs/zh-CN/client-libraries-python/).
   ```sh
   $ pip install pulsar-client==2.7.1
   ```

2. In the code for creating the consumer or producer, configure the prepared access address and token.
<dx-codeblock>
:::  python
from pulsar import Client, AuthenticationToken

# Create the client
client = Client('http://***'
                authentication=AuthenticationToken('eyJh****')) # Replace with the access address (copied from the **Cluster Management** page in the console) and token

# Add a new producer (multiple producers can be created under a single client and should be reused as much as possible)
producer = client.create_producer('persistent://pulsar-****/default/mytopic')
for i in range(10):
    producer.send(('Message-%d' % i).encode('utf-8'))
# Close the client (be sure to close the client if you don't use it for a long time and repossess the connection pool resources in time)
client.close()
:::
</dx-codeblock>


For how to use various features of the Apache Pulsar SDK for Python, see [Pulsar Python client](http://pulsar.apache.org/docs/zh-CN/client-libraries-python/).

