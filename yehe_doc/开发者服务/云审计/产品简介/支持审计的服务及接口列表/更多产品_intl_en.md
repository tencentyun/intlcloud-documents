| Product Name | Operation Name | Resource Type | Event Name |
|------------------|--------------------------------|-----------|------------------------------------------|
| Anti-DDoS               | Getting DDoS attack details of Anti-DDoS Basic                 | bgpip     | CreateSolution                           |
| Anti-DDoS               | Adding layer-4 forwarding rule                       | bgpip     | DeleteSolutionResources                  |
| Anti-DDoS               | Querying whether the Anti-DDoS Advanced instance can be purchased                   | bgpip     | DescribeSolutionResources                |
| Anti-DDoS               | BGP IP - Querying purchase price                    | bgpip     | DescribeSolutionResourceTasks            |
| Anti-DDoS               | BGP IP - Delivering service                      | bgpip     | DescribeSolutions                        |
| Anti-DDoS               | BGP IP - Getting the number of DDoS attacks                | bgpip     | BasicDDoSGetDetails                      |
| Anti-DDoS               | BGP IP - Getting DDoS attack details                | bgpip     | BGPIPAddTransRules                       |
| Anti-DDoS               | BGP IP - Getting DDoS attack statistics                | bgpip     | BgpipCheckCreate                         |
| Anti-DDoS               | BGP IP - Querying order by order number                   | bgpip     | BgpipCreatePrice                         |
| Anti-DDoS               | BGP IP - Getting the details of Anti-DDoS Advanced instance                | bgpip     | BgpipCreateResource                      |
| Anti-DDoS               | BGP IP - Getting the list of Anti-DDoS Advanced instances               | bgpip     | BGPIPDDoSGetCounter                      |
| Anti-DDoS               | BGP IP - Getting the numbers of days in service and attacks               | bgpip     | BGPIPDDoSGetDetails                      |
| Anti-DDoS               | BGP IP - Getting forwarded traffic statistics                  | bgpip     | BGPIPDDoSGetStatistics                   |
| Anti-DDoS               | BGP IP - Getting rule list                    | bgpip     | BgpipGetIdByTran                         |
| Anti-DDoS               | BGP IP - Getting layer-7 rule                  | bgpip     | BGPIPGetInfo                             |
| Anti-DDoS               | BGP IP - Renewing                      | bgpip     | BGPIPGetServicePacks                     |
| Anti-DDoS               | Querying the information of IP bound to multi-IP instance                    | bgpip     | BGPIPGetServiceStatistics                |
| Anti-DDoS               | Getting the maximum number of layer-7 rules that can be added                 | bgpip     | BGPIPGetTransFlow                        |
| Anti-DDoS               | Getting custom CC policy list                    | bgpip     | BGPIPGetTransRules                       |
| Anti-DDoS               | Getting unblocking time                         | bgpip     | BGPIPGetWadTransRules                    |
| Anti-DDoS               | Getting URL allowlist                       | bgpip     | BgpipRenewResource                       |
| Queue Model             | Clearing message in message queue                     | cmqqueue  | transfer                                 |
| Queue Model             | Creating queue                           | cmqqueue  | viewClients                              |
| Queue Model             | Deleting queue                           | cmqqueue  | viewDeals                                |
| Queue Model             | Getting queue attribute                         | cmqqueue  | viewMenu                                 |
| Queue Model             | Modifying queue attribute                         | cmqqueue  | viewMessage                              |
| Queue Model             | Rewinding queue                           | cmqqueue  | ClearQueue                               |
| Queue Model             | Modifying queue attribute                         | cmqqueue  | CreateQueue                              |
| Topic Model             | Creating topic                           | cmqtopic  | DeleteQueue                              |
| Topic Model             | Deleting topic                           | cmqtopic  | GetQueueAttributes                       |
| Topic Model             | Getting topic attribute                         | cmqtopic  | ModifyQueueAttribute                     |
| Topic Model             | Modifying topic attribute                         | cmqtopic  | RewindQueue                              |
| Topic Model             | Modifying topic attribute                         | cmqtopic  | SetQueueAttributes                       |
| MediaLive             | Creating media service user                      | mdl       | GetRule                                  |
| MediaLive             | Creating media channel                        | mdl       | GetRules                                 |
| MediaLive             | Creating media input                        | mdl       | GetTopics                                |
| MediaLive             | Deleting media live streaming channel                      | mdl       | GetUser                                  |
| MediaLive             | Deleting media input                        | mdl       | PublishMsg                               |
| MediaLive             | Querying the information of media live streaming channel                    | mdl       | ActivateMediaService                     |
| MediaLive             | Querying channel alarm information                      | mdl       | CreateMediaLiveChannel                   |
| MediaLive             | Querying input statistics                     | mdl       | CreateMediaLiveInput                     |
| MediaLive             | Querying channel output statistics                   | mdl       | DeleteMediaLiveChannel                   |
| MediaLive             | Querying the information of media live streaming channels in batches                  | mdl       | DeleteMediaLiveInput                     |
| MediaLive             | Querying media input                        | mdl       | DescribeMediaLiveChannel                 |
| MediaLive             | Querying the information of media inputs in batches                    | mdl       | DescribeMediaLiveChannelAlerts           |
| MediaLive             | Querying input security group                       | mdl       | DescribeMediaLiveChannelInputStatistics  |
| MediaLive             | Querying the information of input security groups in batches                   | mdl       | DescribeMediaLiveChannelOutputStatistics |
| MediaLive             | Querying the activation status of media service user                  | mdl       | DescribeMediaLiveChannels                |
| MediaLive             | Modifying the information of media live streaming channel                    | mdl       | DescribeMediaLiveInput                   |
| MediaLive             | Updating media input                        | mdl       | DescribeMediaLiveInputs                  |
| MediaLive             | Updating input security group                       | mdl       | DescribeMediaLiveInputSecurityGroup      |
| MediaLive             | Enabling media live streaming channel                      | mdl       | DescribeMediaLiveInputSecurityGroups     |
| MediaLive             | Disabling media live streaming channel                      | mdl       | DescribeMediaServiceActivateState        |
| MediaPackage             | Creating media package channel                      | mdp       | ModifyMediaLiveChannel                   |
| MediaPackage             | Creating media package channel endpoint                    | mdp       | ModifyMediaLiveInput                     |
| MediaPackage             | Modifying media package channel endpoint                    | mdp       | ModifyMediaLiveInputSecurityGroup        |
| MediaPackage             | Deleting media package channels in batches                    | mdp       | StartMediaLiveChannel                    |
| MediaPackage             | Querying media package channel information                    | mdp       | StopMediaLiveChannel                     |
| MediaPackage             | Querying the list of media package channel information                  | mdp       | CreateMediaPackageChannel                |
| MediaPackage             | Modifying the information of media package channel                    | mdp       | CreateMediaPackageChannelEndpoint        |
| MediaPackage             | Modifying media package channel endpoint                    | mdp       | DeleteMediaPackageChannelEndpoints       |
| MediaPackage             | Modifying the input authentication information of media package channel                | mdp       | DeleteMediaPackageChannels               |