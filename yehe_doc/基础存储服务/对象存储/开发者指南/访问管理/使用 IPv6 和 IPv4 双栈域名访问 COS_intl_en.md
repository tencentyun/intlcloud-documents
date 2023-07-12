## Overview

As the internet booms, IPv4 addresses will be used up soon. Actually, the IPv4 addresses managed by the Internet Assigned Numbers Authority (IANA) were exhausted on January 31, 2011, and issuable IPv4 addresses of other five Regional Internet Registries will also run out by the end of 2020.

Therefore, the Internet Engineering Task Force (IETF) developed the next-generation network protocol of IPv4, i.e., Internet Protocol version 6 (IPv6). After nearly 10 years of discussion, IPv6 was officially announced in December 1998 as an internet standard ([RFC 2460](https://tools.ietf.org/html/rfc2460)). Compared with IPv4, IPv6 has two significant advantages:

1. It has a larger address space. The length of an IPv6 address is 128 bits, compared with 32 bits in IPv4. This eliminates the dependence on network address translation, enables more devices to access the internet, and thus serves as a cornerstone in the development of the Internet of Everything.
2. It has securer transfer protocols that forcibly require transfer encryption and make access securer and more reliable.

IPv6 is the basis for future expansion of internet addresses. However, switching to IPv6 addresses requires a lot of work, as changes have to be made to routers, firewalls, internal systems, relevant applications, etc. Currently, dual-stack domain name access is used in many main technology roadmaps. IPv4 is expected to be supported before 2025 to allow enough time for transition to IPv6. Based on this, COS provides IPv6/IPv4 dual-stack domain names to facilitate IPv6 and IPv4 clients to read and write resources in the cloud at any time.

## Accessing COS with IPv6/IPv4 dual-stack domain name

COS currently supports IPv6/IPv4 dual-stack domain names. You only need to change your existing access domain name to a dual-stack one, and then you can access your COS resources over IPv6 from a client.

Currently, COS has provided dual-stack domain names in the Shanghai region, which can be accessed from both IPv6 and IPv4 clients. The access domain name is in the following format:

```sh
<BucketName-APPID>.cos-dualstack.<Region>.myqcloud.com
```

For a dual-stack domain name in Shanghai, you only need to replace the `<Region>` parameter with `ap-shanghai`:

```sh
<BucketName-APPID>.cos-dualstack.ap-shanghai.myqcloud.com
```

Taking the Shanghai region as an example, if you have created a bucket named `camera_iotdevice_id-125000000000` that stores a video file `record_hashid.mov`, then the dual-stack domain name of the file will be as follows:

```sh
https://camera_iotdevice_id-125000000000.cos-dualstack.ap-shanghai.myqcloud.com/record_hashid.mov
```
