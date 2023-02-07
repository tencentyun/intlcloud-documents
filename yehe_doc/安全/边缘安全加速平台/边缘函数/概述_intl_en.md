Tencent Cloud Edge Functions provides a serverless code execution environment for the edge nodes of Tencent Cloud EdgeOne. This way, you can focus on writing business function code and configuring triggering rules, without the need to configure or manage infrastructure such as servers. The written code can be elastically and securely executed on the edge nodes that are closest to users.

![](https://qcloudimg.tencent-cloud.cn/raw/d90b8f67ff843ee7ecef4d80cc7393dc.png)

## How It Works
![](https://qcloudimg.tencent-cloud.cn/raw/9e4fa13ee0d276ba435786bd983780e8.png)

You can develop JavaScript functions and deploy them to the edge nodes of Tencent Cloud EdgeOne.

1. If a client request does not hit the configured function triggering rule, the request is handled in the following process:  
  - `(1)` The client request is sent to the gateway of an edge node of Tencent Cloud EdgeOne. > `(2)` The cache of the node responds if the requested content already exists in the cache. > `(3)` The origin server responds if the requested content does not exist in the cache.
2. If a client request hits the configured function triggering rule, the request is handled in one of the following processes:    
  - `(1)` The client request is sent to the gateway of an edge node of Tencent Cloud EdgeOne. > `(4)` Edge Functions receives and executes the JavaScript code. > `(5)` Subrequests access the cache. > `(3)` The origin server responds if the requested content does not exist in the cache.  
  - `(1)` The client request is sent to the gateway of an edge node of Tencent Cloud EdgeOne. > `(4)` Edge Functions receives and executes the JavaScript code. > `(6)` Subrequests access the public network service.


## Benefits
#### Distributed deployment
Tencent Cloud EdgeOne supports more than 2,800 edge nodes. Edge Functions is deployed on edge nodes in distributed mode.
#### Ultra-low latency
Client requests are automatically scheduled to the edge nodes that are closest to users. If triggering rules are hit, edge functions are triggered to process the requests and return results to the client. This helps significantly reduce the client access latency.
#### Elastic scaling
Edge Functions schedules requests to edge nodes that are allocated sufficient computing resources based on the proximity of the user when spikes occur in client requests.
#### Serverless architecture
The serverless architecture of Edge Functions eliminates the need to focus on the maintenance of the memory, CPU, and network of servers and other infrastructure resources. You can focus on the development of business code.

## Use Cases

![](https://qcloudimg.tencent-cloud.cn/raw/c7df61d9526b26b95fc643f1569e5939.png)
