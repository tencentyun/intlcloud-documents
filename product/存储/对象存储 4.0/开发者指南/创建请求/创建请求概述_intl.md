## Concept

Tencent Cloud COS is a web-based storage service accessed using the HTTP/HTTPS protocol. You can use the REST API or [COS SDK](https://intl.cloud.tencent.com/document/product/436/6474) to access COS.

Your COS access request must first pass the COS verification and authentication before COS starts to operate the resources. Therefore, depending on whether the identity is identifiable, COS access requests are divided into two types: anonymous requests and requests with signatures.

-  Anonymous request: If the request does not include Authorization or related parameters, or the user identity cannot be identified based on the related characters, the request will be treated as an anonymous request for authentication.
-  Request with signature: A request with a signature must contain the Authorization field in the HTTP header or the request package. The content of the field is generated based on Tencent Cloud security credentials (SecretID and SecretKey) and some eigenvalues of the request via an encryption algorithm.

To access COS using COS SDKs, you only need to configure your security credentials before initiating the request. To access COS using the REST API, calculate the request signature according to [Request Signature](https://intl.cloud.tencent.com/document/api/436/7778) .

## Obtaining Security Credentials

Cloud Access Management (CAM) provides features and services related to accounts and credentials for COS, to help customers manage the permissions to access resources under their Tencent Cloud accounts in a secure way. You can use CAM to create, manage and terminate users (or user groups), and manage other users' permissions to use Tencent Cloud resources through identity management and policy management.

### Security certificates of the primary account

After logging in to the primary account, you can manage and obtain the security credentials (SecretID and SecretKey) of your primary account on the [Cloud API Key](https://console.cloud.tencent.com/cam/capi) page of CAM. The following is a key pair example:

> 36-character access key ID (SecretID): AKIDHZRLB9Ibhdp7Y7gyQq6BOk1997BGmUXg
> 32-character access Key (SecretKey): LYaWIuQmCSZ5ZMniUM6hiaLxHnW6XxRK

The access key can be used to identify the uniqueness of an account. After the signature is generated using the key and the request is sent, Tencent Cloud will identify the identity of the request initiator, and then perform verification and authentication for the identity, resources, operations, and conditions to determine whether to allow the operation.

>The key of the primary account has all the operation permissions for all resources under the primary account. Disclosure of the key may cause loss of your cloud assets, so it is strongly recommended that you create sub-accounts and assign corresponding permissions for them, and then use the keys of sub-accounts to create requests for resource access and management.

### Security certificates of sub-accounts

To manage users and cloud resources under your account in multiple dimensions, you can create multiple sub-accounts under your primary account to implement user-specific permission management. For more information on how to create a sub-account, see [Sub-users](https://intl.cloud.tencent.com/document/product/598/13674) in CAM.

Before using a sub-account to initiate an API request, you need to create a security credential for the sub-account, and then the sub-account will get a unique key pair, which can facilitate the identification of the identity. You can create user policies for different sub-accounts to control their access permissions to resources. You can also create user groups and associate one access policy to a user group to facilitate the central management of user grouping and resources.

> With the corresponding permissions assigned, a sub-account can create or modify resources. The resources still belong to the primary account, and the resource cost will be deducted from the primary account.

### Temporary security credentials

In addition to using security credentials of the primary account or sub-accounts to access resources, you can create roles and use the temporary security credentials of the roles to manage your Tencent Cloud resources. For more information on the role concept and how to use roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420).

As a virtual identity, a role does not have a permanent key. CAM provides a set of STS APIs used to generate temporary security credentials.
For more information on how to use the APIs and relevant examples, see [Using Roles](https://intl.cloud.tencent.com/document/product/598/19419). See [STS API](https://intl.cloud.tencent.com/document/product/598/13895) to learn about how to generate temporary security credentials. Temporary security credentials contain only **limited policies** (operations, resources, and conditions), and are valid for a **limited period** (start and end time), so the generated temporary security credentials can be distributed or used directly.

You can call the API for to generate temporary security credentials and get a temporary key pair (tmpSecretId/tmpSecretKey) and a security token (sessionToken), which form the security credential that can be used to access COS. Here is a temporary security credential example:

> 41-character security token (SecurityToken): 5e776c4216ff4d31a7c74fe194a978a3ff2a42864
> 36-character temporary access key ID (SecretID): AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl
> 32-character temporary access key (SecretKey): VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD

This API also returns the validity period of the temporary security credential via the `expiration` field, which means that this set of security credentials can only be used to initiate requests during this period.

Tencent Cloud COS provides a simple server SDK that can be used to generate temporary keys. You can visit [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk) to obtain the SDK. To initiate the request using the REST API after getting the temporary security credential, you need to specify the value for the `x-cos-security-token` field in the HTTP header or the form-data of the POST request package to identify the security token used by the request, and then use the temporary access key pair to generate the request signature. For more information on how to initiate requests using the COS SDK, see the relevant sections in each SDK documentation.

## Access Domain Name

### REST API

The [Region and Access Domain Name](https://intl.cloud.tencent.com/document/product/436/6224) document provides a list of domain names that can be used to initiate access requests via the REST API.

It is recommended to use virtual hosting domain names to access COS buckets. When you initiate an HTTP request, the bucket to be accessed will be specified through the `Host` header, such as `<BucketName-APPID>.cos.<Region>.myqcloud.com`. Using virtual hosting domain names realizes the same feature as the "root" of a virtual server. Virtual hosting domain names can be used to host files such as favicon.ico, robots.txt, and crossdomain.xml, which are the content that many applications will retrieve from the "root" of the virtual server by default when identifying a hosted website.

You can also use a path request to access a bucket, such as `cos.<region>.myqcloud.com/<BucketName-APPID>/`. The request Host and the signature must use `cos.<region>.myqcloud.com`. SDK does not support this access method by default.

### Domain name of static websites

If you enable the static website feature, a virtual hosting domain name will be assigned for you to use relevant features. Unlike the REST API, the domain name of static website only supports a few operations, such as GET/HEAD/OPTIONS Object, in addition to specific index pages, error pages and redirection configurations. Uploading or configuring resources is not supported.

The format of a domain name of a static website is `<BucketName-APPID>.cos-website.<Region>.myqcloud.com`，. You can also log in to the console and go to the bucket's **Basic Configuration** -> **Static Website Configuration** to get the domain name.

## COS Access via Private Network and Public Network

The access domain names of COS adopt intelligent DNS resolution. For COS access via Internet (including different ISPs), we will detect and select the optimal linkage for you to access COS. If you have deployed a service in Tencent Cloud to access COS, the access in the same region will be automatically directed to the private network address. The cross-region access is not supported in the private network and the COS domain name is resolved to the public network address by default.

### How to determine an access via private network

Tencent Cloud products within the same region access each other over a private network by default and no traffic fee is charged for these connections. For this reason, it is recommended to choose the same region when you purchase different Tencent Cloud products for cost saving.

The following shows how to determine whether it is an access via private network:

For example, when a CVM access COS, to determine whether a private network is used to access COS, use the `nslookup` command on the CVM to resolve the COS domain name. If a private network IP is returned, the access between CVM and COS is over a private network; otherwise, it is over a public network.

>Generally, a private IP address takes the form of `10.*.*.*` or `100.*.*.*`, and a VPC IP address takes the form of `169.254.*.*`.

Assume that `mybucket-1250000000.cos.ap-guangzhou.myqcloud.com` is the address of target bucket, and the `Address: 10.148.214.13` below it indicates the access is over the private network.

```shell
nslookup mybucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   mybucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   mybucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

### Testing connectivity

#### Basic connectivity test

COS uses the HTTP protocol to provide services. You can use the most basic tool `telnet` to test the connectivity to port 80 of the COS access domain.

An example of access through the public network:

```shell
telnet mybucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 14.119.113.22...
Connected to gz.file.myqcloud.com.
Escape character is '^]'.
```

An example of access through Tencent Cloud CVMs (basic network) within the same region:

```shell
telnet mybucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 10.148.214.14...
Connected to 10.148.214.14.
Escape character is '^]'.
```

An example of access through Tencent Cloud CVMs (VPC) within the same region:

```shell
telnet mybucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 169.254.0.47....
Connected to 169.254.0.47.
Escape character is '^]'.
```

Regardless of the access environment, if the command returns the `Escape character is '^]'.` field, it indicates that the connection is successful.

#### Test via the Internet

Since the access to COS over the Internet involves the ISP network, which may prohibit you from testing connectivity using such tools as `ping` or `traceroute` of the ICMP protocol, so it is recommended to use the tools of the TCP protocol to test connectivity.
>The access via the Internet may involve multiple network environments. If the access is not smooth, check your local network linkage, or contact the local ISP.

If your ISP allows you to use the ICMP protocol, you can use the `ping`, `traceroute` or `mtr` tools to check your linkage. Otherwise, you can use the `psping` (Windows environment; download at the Microsoft official website) or such tools as `tcping` (cross-platform software) to test the latency.

#### Test via the private network

If you access the COS over the Tencent Cloud VPC in the same region, you may be unable to test connectivity using such tools as `ping` or `traceroute` of the ICMP protocol. It is recommended that you use the `telnet` command in the basic connectivity test to perform the testing.

You can also use the tools such as `psping` or `tcping` to test the latency to port 80 of the access domain. Before the test, make sure that the access domain name has been correctly resolved to the private network address using the `nsloopup` command.

