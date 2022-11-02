
This document offers answers to questions that you may have when [building a deep learning container image](https://intl.cloud.tencent.com/document/product/457/42059) and [running deep learning in EKS](https://intl.cloud.tencent.com/document/product/457/42060).


### How does a container access the public network?

As you may need to download training datasets during a task, access to the public network may be required. However, a container in its initial status cannot access the public network, and if you directly run a command with dataset download, the following error will be reported:

```shell
W tensorflow/core/platform/cloud/google_auth_provider.cc:184] All attempts to get a Google authentication bearer token failed, returning an empty token. Retrieving token from files failed with "Not found: Could not locate the credentials file.". Retrieving token from GCE failed with "Failed precondition: Error executing an HTTP request: libcurl code 6 meaning 'Couldn't resolve host name', error details: Could not resolve host: metadata".
E tensorflow/core/platform/cloud/curl_http_request.cc:614] The transmission  of request 0x5b328e0 (URI: https://www.googleapis.com/storage/v1/b/tfds-data/o/dataset_info%2Fmnist%2F3.0.1?fields=size%2Cgeneration%2Cupdated) has been stuck at 0 of 0 bytes for 61 seconds and will be aborted....
```

For the above problem, two public network access methods are provided:

- **NAT Gateway**: it is suitable for scenarios where many Pods in a VPC need to communicate with the public network. Please configure as instructed in [Accessing Internet Through NAT Gateway](https://intl.cloud.tencent.com/document/product/457/38369).
>!The created NAT gateway and route table need to be in the same region and VPC as the EKS cluster.
- **EIP**: it is suitable for scenarios where one or a few Pods need to interconnect with the public network. 

