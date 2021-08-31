## Overview


This document describes how to create instances and topics in the CKafka console.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [purchased a CVM](https://buy.cloud.tencent.com/cvm).

## Directions

### Step 1. Create an instance and add a public route.

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** in the left navigation pane and then click **Create** to go to the instance purchase page and enter the purchase information.
   ![](https://main.qcloudimg.com/raw/ec7c52c012f1cf71940f9993921b0748.png)

   >?
   >- We recommend that you choose the private network of an existing CVM so as to save the step of adding routes to connect to Kafka.
   >- If the private network you choose is not the network of your CVM or other resources, you can click [Adding a routing policy](https://intl.cloud.tencent.com/document/product/597/32555) in **Access Mode** to add a route.
   >- If you want to access CKafka via a public network, you can click [Adding a routing policy](https://intl.cloud.tencent.com/document/product/597/32555) in **Access Mode** to add a public route. Public network access requires the configuration of ACL policies for topics. In this document, a public network is used as an example.

3. Click **Buy Now**, and the instance created appears in the instance list in about 3-5 minutes.
   ![](https://main.qcloudimg.com/raw/b8540b7589f70a40b8ad3ab7fac91f86.png)

4. Click the ID/name of your instance to go to the details page and, in the **Access Mode** section, click **Adding a routing policy** to add a public route.
   ![](https://main.qcloudimg.com/raw/39733cf43129ef52cb707e4e564eed6c.png)

Then you get the domain name and port for public network access.
![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png)


### Step 2. Create a topic and an ACL policy.

1. In the instance details page, select **Topic Management**, click **Create**, enter a name and select the number of partitions and replicas, and create a topic.
	 ![](https://main.qcloudimg.com/raw/8451c29a64cc1eed19bebb6ba2d6f939.png)

2. In the instance details page, select **User Management**, and click **Create** to add a user and set the user name and password.
	 ![](https://main.qcloudimg.com/raw/bf56ee0f3f53dda9ce9c0619a5c05cbc.png)

3. In the **ACL Policy Management** tab, find the topic created, and click **Edit ACL Policy** in the *Operation* column to create an ACL policy.
   ![](https://main.qcloudimg.com/raw/88b8f12af12c42640bc4e02a485e167f.png)
