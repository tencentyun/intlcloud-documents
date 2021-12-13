## Overview

TDMQ for Pulsar 2.7.1 and above clusters already support Apache Pulsar SDK for C++. This document describes how to access the SDK.

## Prerequisites

- Get the access address
  Copy the access address on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the TDMQ for Pulsar console.

- Get the token
  Configure the role and permission as instructed in [Role and Authentication](https://intl.cloud.tencent.com/document/product/1110/42936) and get the token of the role.


## Directions

1. Install the Pulsar C++ library in your client environment as instructed in [Pulsar C++ client](http://pulsar.apache.org/docs/en/client-libraries-cpp/).
   ```sh
   brew install libpulsar
   ```

2. In the code for creating the client, configure the prepared access address and token. The following shows an example of message production.
<dx-codeblock>
::: c++

#include <pulsar/Client.h>

// Create a client
pulsar::ClientConfiguration config;
config.setAuth(pulsar::AuthToken::createWithToken("eyJh****"));

pulsar::Client client("http://***", config); // Replace with the access address

// Add a new producer (multiple producers can be created under a single client and should be reused as much as possible)
Producer producer;
Result result = client.createProducer("persistent://pulsar-****/default/mytopic", producer);
if (result != ResultOk) {
				LOG_ERROR("Error creating producer: " << result);
				return -1;
}

// Send a message
for (int i = 0; i < 10; i++){
				Message msg = MessageBuilder().setContent("my-message").build();
				Result res = producer.send(msg);
				LOG_INFO("Message sent: " << res);
}

// Close the client (be sure to close the client if you don't use it for a long time and repossess the connection pool resources in time)
client.close();
:::
</dx-codeblock>


For how to use various features of the Apache Pulsar SDK for C++, see [Pulsar C++ client](http://pulsar.apache.org/docs/en/client-libraries-cpp/).

