## Overview

TDMQ for Pulsar provides the same JWT authentication method used by native Pulsar, which allows you to access TDMQ for Pulsar resources by configuring the token in the client parameters. For directions on how to configure the relationships between different role tokens and TDMQ for Pulsar resources in the console, see [Roles and Permissions](https://intl.cloud.tencent.com/document/product/1110/42936).

This document describes how to configure JWT authentication in a TDMQ for Pulsar client, so that you can securely use the client to produce and consume messages. You can also add a token when creating a client.

## Authentication Configuration

### Java client

Configure JWT authentication in a Java client:
<dx-tabs>
::: Access sample for cluster on v2.7.1 or above
```  java
PulsarClient client = PulsarClient.builder()
     // Access address, which can be copied from **Access Address** in the **Operation** column on the **Cluster Management** page
     .serviceUrl("http://*") 
		// Replace it with the role token displayed on the **Role Management** page
     .authentication(AuthenticationFactory.token("eyJh****")) 
     .build();
```
:::
::: Access sample for cluster on v2.6.1
```  java
PulsarClient client = PulsarClient.builder()
      // Access address, which can be copied from the access point list in **Cluster Management**
		 .serviceUrl("pulsar://*.*.*.*:6000/")
		 // Replace it with the role token displayed on the **Role Management** page
      .authentication(AuthenticationFactory.token("eyJh****")) 
		 // Replace the value of `custom:` with the route ID in the access point list in **Cluster Management**
      .listenerName("custom:1********0/vpc-******/subnet-********")
      .build();
```
:::
</dx-tabs>





### Go client

Configure JWT authentication in a Go client:
<dx-tabs>
::: Access sample for cluster on v2.7.1 or above
```  go
client, err := NewClient(ClientOptions{
      // Access address, which can be copied from the access point list in **Cluster Management**
		 URL:            "http://*",  
		 // Replace it with the role token displayed on the **Role Management** page
      Authentication: NewAuthenticationToken("eyJh****"),  
})
```
:::
::: Access sample for cluster on v2.6.1
```  go
client, err := NewClient(ClientOptions{
      // Access address, which can be copied from the access point list in **Cluster Management**
		 URL:            "pulsar://*.*.*.*:6000",  
		 // Replace it with the role token displayed on the **Role Management** page
      Authentication: NewAuthenticationToken("eyJh****"),  
		 // Replace the value of `custom:` with the route ID in the access point list in **Cluster Management**
      ListenerName:   "custom:1300*****0/vpc-******/subnet-********",  
})
```
:::
</dx-tabs>











