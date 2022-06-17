## Overview
As one of the most popular open-source container engine, Docker allows developers to package applications and dependencies into lightweight, portable containers conveniently and efficiently for faster application delivery, deployment, migration, and scaling. This document describes how to use the Docker CE application image to build a Docker container environment. The Docker image source has been set to Tencent Cloud Docker image source by default, which can accelerate Docker image downloads.

>?The underlying layer of the sample Docker CE image in this document is based on CentOS 7.6 64-bit. Application images are subject to updates from time to time, and the actual image information on the purchase page shall prevail.


## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse) and configure the following parameters:
 - **Region** and **Availability zone**: Select the region and AZ near your target users to reduce the network latency and improve their access speed.
 - **Image**: Select **Official image** > **Docker CE application image**.
 - **Instance bundle**: Select an instance bundle according to the required instance configuration (including CPU, memory, system disk, bandwidth, and monthly traffic).
 - **Instance name**: Enter a custom instance name. If it is left empty, the selected image name will be used as the name by default. When multiple instances are created in a batch, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and create three instances, the three instances are named "LH1", "LH2", and "LH3".
 - **Purchase period**: Default to **1 month**.
 - **Quantity**: Default to **1**.
2. Click **Buy now** to submit your order and make the payment as prompted.

## Relevant Operations
### Enabling HTTPS access
You can install an SSL certificate and enable HTTPS access for your website as instructed in [Installing Certificate on NGINX Server](https://intl.cloud.tencent.com/document/product/1103/47406).


