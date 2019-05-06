

## Basis Info APIs
| API| Description |
| ------------------------------ | ------------------------------- |
| [BGPIPGetInfo](https://cloud.tencent.com/document/product/1014/31246)             | Gets details about a specific Anti-DDoS Advanced instance |
| [BGPIPRename](https://cloud.tencent.com/document/product/1014/31245)                    | Renames a specific Anti-DDoS Advanced instance |
| [BGPIPSetCCThreshold](https://cloud.tencent.com/document/product/1014/31244)            | Sets a CC defense threshold for a specific Anti-DDoS Advanced instance |
| [BGPIPSetElasticProtectionLimit](https://cloud.tencent.com/document/product/1014/31243) | Sets an elastic defense limit for a specific Anti-DDoS Advanced instance |
| [AddCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31242)            | Adds a single CC custom policy |
| [EditCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31241)           | Edits a single CC custom policy |
| [GetCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31240)            | Gets a single CC custom policy |
| [GetCustomCCStrategyList](https://cloud.tencent.com/document/product/1014/31239)        | Gets a CC custom policy list |
| [RemoveCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31238)         | Removes a single CC custom policy |
| [SetCustomCCStrategyStatus](https://cloud.tencent.com/document/product/1014/31237)      | Enables or disables a single CC custom policy |
| [OpenDomainCCProtection](https://cloud.tencent.com/document/product/1014/31236)         | Enables domain rule CC defense |
| [CloseDomainCCProtection](https://cloud.tencent.com/document/product/1014/31235)        | Disables domain rule CC defense |

## Defense Info APIs
| API Name | Description |
| ----------------------- | ----------------------------------------------------------- |
| [BGPIPDDoSGetCounter](https://cloud.tencent.com/document/product/1014/31253)     | Gets the number of DDoS attacks suffered by a specific Anti-DDoS Advanced instance, the peak attack size, and the number of elastic defenses enabled for this instance |
| [BGPIPDDoSGetStatistics](https://cloud.tencent.com/document/product/1014/31252)  | Gets the traffic statistics of DDoS attacks on a specific Anti-DDoS Advanced instance |
| [BGPIPDDoSGetDetails](https://cloud.tencent.com/document/product/1014/31251)     | Gets the details of DDoS attack traffic on a specific Anti-DDoS Advanced instance |
| [BGPIPCCGetCounter](https://cloud.tencent.com/document/product/1014/31250)       | Gets the number of CC attacks suffered by a specific Anti-DDoS Advanced instance and the peak attack size |
| [BGPIPCCGetStatistics](https://cloud.tencent.com/document/product/1014/31249)    | Gets the statistic chart of CC attack traffic on a specific Anti-DDoS Advanced instance |
| [BGPIPCCGetDetails](https://cloud.tencent.com/document/product/1014/31248)       | Gets the details of CC attack traffic on a specific Anti-DDoS Advanced instance |
| [BGPIPTransGetStatistics](https://cloud.tencent.com/document/product/1014/31247) | Gets the statistic chart of the traffic forwarded from an Anti-DDoS Advanced instance to the servers outside Tencent Cloud |

## Service List APIs
| API | Description |
| ------------------------- | ----------------------------------------- |
| [BGPIPGetServicePacks](https://cloud.tencent.com/document/product/1014/31261)      | Gets a list of all the Anti-DDoS Advanced instances under a given user name |
| [BGPIPGetServiceStatistics](https://cloud.tencent.com/document/product/1014/31262) | Gets the number of usage days and number of defenses of Anti-DDoS Advanced |

## Forwarding Rule APIs
| API | Description |
| ------------------------ | ----------------------------------------- |
| [BGPIPAddTransRules](https://cloud.tencent.com/document/product/1014/31270)       | Adds a Layer-4 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPEditTransRules](https://cloud.tencent.com/document/product/1014/31269)      | Edits a specific Layer-4 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPGetTransRules](https://cloud.tencent.com/document/product/1014/31268)       | Gets the Layer-4 forwarding rule list for a specific Anti-DDoS Advanced instance |
| [BGPIPDeleteTransRules](https://cloud.tencent.com/document/product/1014/31267)    | Removes a specific Layer-4 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPAddWadTransRules](https://cloud.tencent.com/document/product/1014/31266)    | Adds a Layer-7 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPEditWadTransRules](https://cloud.tencent.com/document/product/1014/31265)   | Edits a specific Layer-7 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPGetWadTransRules](https://cloud.tencent.com/document/product/1014/31263)    | Gets the Layer-7 forwarding rule list for an Anti-DDoS Advanced instance |
| [BGPIPDeleteWadTransRules](https://cloud.tencent.com/document/product/1014/31264) | Removes a specific Layer-7 forwarding rule for a specific Anti-DDoS Advanced instance |

## Whitelist APIs
| API | Description |
| ---------------- | --------------------------------------------- |
| [GetWhiteUrl](https://cloud.tencent.com/document/product/1014/31277)      | Gets the whitelist for a specific Anti-DDoS Advanced instance |
| [AddWhiteUrl](https://cloud.tencent.com/document/product/1014/31276)      | Adds the URL whitelist for a specific Anti-DDoS Advanced instance |
| [RemoveWhiteUrl](https://cloud.tencent.com/document/product/1014/31275)   | Removes the URL whitelist for a specific Anti-DDoS Advanced instance |
| [GetSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31274)    | Gets the source IP whitelist for a specific Anti-DDoS Advanced instance |
| [AddSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31273)    | Adds the source IP whitelist for a specific Anti-DDoS Advanced instance |
| [RemoveSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31272) | Removes the source IP whitelist for a specific Anti-DDoS Advanced instance |

## Blacklist APIs
| API | Description |
| ---------------- | --------------------------------------------- |
| [AddSrcBlackIP](https://cloud.tencent.com/document/product/1014/31278)    | Adds the source IP blacklist for a specific Anti-DDoS Advanced instance |
| [RemoveSrcBlackIP](https://cloud.tencent.com/document/product/1014/31279) | Removes an IP from the blacklist of the specified Anti-DDoS Advanced instance |


