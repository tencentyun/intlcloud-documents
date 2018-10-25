Tencent Cloud products within the same region access each other over a private network by default. It is recommended that you choose the same region if possible when purchasing cloud products or performing API operations, to reduce public network traffic charges.

In the following, we use the example of a CVM accessing CAS, to determine whether a private network is used to access CAS. On the CVM, use the `nslookup` command to resolve the request address of the vault created on CAS. If a private network IP is returned, it means the access between CVM and CAS is over a private network; otherwise, it is over a public network.
Generally, a private IP address takes the form of `10.*.*.*` or `100.*.*.*`. A VPC network can take the form of `169.*.*.*`.
If `cas.ap-chengdu.myqcloud.com` is the request address of the vault, `Address: 10.148.214.13` below means the access is from a private network.

```
nslookup cas.ap-chengdu.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65#53

Name:   cas.ap-chengdu.myqcloud.com
Address: 10.148.214.13
Name:   cas.ap-chengdu.myqcloud.com
Address: 10.148.214.14
```

