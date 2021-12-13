## Overview

TDMQ for Pulsar 2.7.1 and above clusters already support Apache Pulsar SDK for Node.js. This document describes how to access the SDK.

## Prerequisites

- Get the access address
  Copy the access address on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the TDMQ for Pulsar console.
	
- Get the token
  Configure the role and permission as instructed in [Role and Authentication](https://intl.cloud.tencent.com/document/product/1110/42936) and get the token of the role.


## Directions

1. Install the Node.js client in your client environment as instructed in [Pulsar Node.js client](http://pulsar.apache.org/docs/zh-CN/client-libraries-node/).
   ```go
   $ npm install pulsar-client
   ```

2. In the code for creating the Node.js client, configure the prepared access address and token.
<dx-codeblock>
:::  go
   const Pulsar = require('pulsar-client');
   
   (async () => {
     const client = new Pulsar.Client({
       serviceUrl: 'http://*', // Replace with the access address (copied from the **Cluster Management** page in the console)
       authentication:    Pulsar.NewAuthenticationToken("eyJh**"), // Replace with the token
     });
   
     await client.close();
   })();
:::
</dx-codeblock>


For how to use various features of the Apache Pulsar SDK for Node.js, see [Pulsar Node.js client](http://pulsar.apache.org/docs/zh-CN/client-libraries-node/).

