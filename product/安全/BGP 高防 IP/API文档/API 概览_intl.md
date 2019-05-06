## Basis Info APIs
| API| Description |
| ------------------------------ | ------------------------------- |
| [BGPIPGetInfo](https://intl.cloud.tencent.com/document/product/297/14754)             | Gets details about a specific Anti-DDoS Advanced instance |
| [BGPIPRename](https://intl.cloud.tencent.com/document/product/297/14692)                    | Renames a specific Anti-DDoS Advanced instance |
| [BGPIPSetCCThreshold](https://intl.cloud.tencent.com/document/product/297/14693)            | Sets a CC defense threshold for a specific Anti-DDoS Advanced instance |
| [BGPIPSetElasticProtectionLimit](https://intl.cloud.tencent.com/document/product/297/14694) | Sets an elastic defense limit for a specific Anti-DDoS Advanced instance |
| [AddCustomCCStrategy](https://intl.cloud.tencent.com/document/product/297/14699)            | Adds a single CC custom policy |
| [EditCustomCCStrategy](https://intl.cloud.tencent.com/document/product/297/14736)           | Edits a single CC custom policy |
| [GetCustomCCStrategy](https://intl.cloud.tencent.com/document/product/297/14737)            | Gets a single CC custom policy |
| [GetCustomCCStrategyList](https://intl.cloud.tencent.com/document/product/297/14738)        | Gets a CC custom policy list |
| [RemoveCustomCCStrategy](https://intl.cloud.tencent.com/document/product/297/14739)         | Removes a single CC custom policy |
| [SetCustomCCStrategyStatus](https://intl.cloud.tencent.com/document/product/297/14740)      | Enables or disables a single CC custom policy |
| [OpenDomainCCProtection](https://intl.cloud.tencent.com/document/product/297/14763)         | Enables domain rule CC defense |
| [CloseDomainCCProtection](https://intl.cloud.tencent.com/document/product/297/14764)        | Disables domain rule CC defense |

## Defense Info APIs
| API Name | Description |
| ----------------------- | ----------------------------------------------------------- |
| [BGPIPDDoSGetCounter](https://intl.cloud.tencent.com/document/product/297/14742)     | Gets the number of DDoS attacks suffered by a specific Anti-DDoS Advanced instance, the peak attack size, and the number of elastic defenses enabled for this instance |
| [BGPIPDDoSGetStatistics](https://intl.cloud.tencent.com/document/product/297/14743)  | Gets the traffic statistics of DDoS attacks on a specific Anti-DDoS Advanced instance |
| [BGPIPDDoSGetDetails](https://intl.cloud.tencent.com/document/product/297/14744)     | Gets the details of DDoS attack traffic on a specific Anti-DDoS Advanced instance |
| [BGPIPCCGetCounter](https://intl.cloud.tencent.com/document/product/297/14746)       | Gets the number of CC attacks suffered by a specific Anti-DDoS Advanced instance and the peak attack size |
| [BGPIPCCGetStatistics](https://intl.cloud.tencent.com/document/product/297/14747)    | Gets the statistic chart of CC attack traffic on a specific Anti-DDoS Advanced instance |
| [BGPIPCCGetDetails](https://intl.cloud.tencent.com/document/product/297/14748)       | Gets the details of CC attack traffic on a specific Anti-DDoS Advanced instance |
| [BGPIPTransGetStatistics](https://intl.cloud.tencent.com/document/product/297/14749) | Gets the statistic chart of the traffic forwarded from an Anti-DDoS Advanced instance to the servers outside Tencent Cloud |

## Service List APIs
| API | Description |
| ------------------------- | ----------------------------------------- |
| [BGPIPGetServicePacks](https://intl.cloud.tencent.com/document/product/297/14751)      | Gets a list of all the Anti-DDoS Advanced instances under a given user name |
| [BGPIPGetServiceStatistics](https://intl.cloud.tencent.com/document/product/297/14752) | Gets the number of usage days and number of defenses of Anti-DDoS Advanced |

## Forwarding Rule APIs
| API | Description |
| ------------------------ | ----------------------------------------- |
| [BGPIPAddTransRules](https://intl.cloud.tencent.com/document/product/297/14757)       | Adds a Layer-4 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPEditTransRules](https://intl.cloud.tencent.com/document/product/297/14758)      | Edits a specific Layer-4 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPGetTransRules](https://intl.cloud.tencent.com/document/product/297/14755)       | Gets the Layer-4 forwarding rule list for a specific Anti-DDoS Advanced instance |
| [BGPIPDeleteTransRules](https://intl.cloud.tencent.com/document/product/297/14756)    | Removes a specific Layer-4 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPAddWadTransRules](https://intl.cloud.tencent.com/document/product/297/14759)    | Adds a Layer-7 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPEditWadTransRules](https://intl.cloud.tencent.com/document/product/297/14760)   | Edits a specific Layer-7 forwarding rule for a specific Anti-DDoS Advanced instance |
| [BGPIPGetWadTransRules](https://intl.cloud.tencent.com/document/product/297/14762)    | Gets the Layer-7 forwarding rule list for an Anti-DDoS Advanced instance |
| [BGPIPDeleteWadTransRules](https://intl.cloud.tencent.com/document/product/297/14761) | Removes a specific Layer-7 forwarding rule for a specific Anti-DDoS Advanced instance |

## Whitelist APIs
| API | Description |
| ---------------- | --------------------------------------------- |
| [GetWhiteUrl](https://intl.cloud.tencent.com/document/product/297/14788)      | Gets the whitelist for a specific Anti-DDoS Advanced instance |
| [AddWhiteUrl](https://intl.cloud.tencent.com/document/product/297/14789)      | Adds the URL whitelist for a specific Anti-DDoS Advanced instance |
| [RemoveWhiteUrl](https://intl.cloud.tencent.com/document/product/297/14790)   | Removes the URL whitelist for a specific Anti-DDoS Advanced instance |
| [GetSrcWhiteIP](https://intl.cloud.tencent.com/document/product/297/14791)    | Gets the source IP whitelist for a specific Anti-DDoS Advanced instance |
| [AddSrcWhiteIP](https://intl.cloud.tencent.com/document/product/297/14792)    | Adds the source IP whitelist for a specific Anti-DDoS Advanced instance |
| [RemoveSrcWhiteIP](https://intl.cloud.tencent.com/document/product/297/14793) | Removes the source IP whitelist for a specific Anti-DDoS Advanced instance |

## Blacklist APIs
| API | Description |
| ---------------- | --------------------------------------------- |
| [AddSrcBlackIP](https://intl.cloud.tencent.com/document/product/297/14795)    | Adds the source IP blacklist for a specific Anti-DDoS Advanced instance |
| [RemoveSrcBlackIP](https://intl.cloud.tencent.com/document/product/297/14796) | Removes an IP from the blacklist of the specified Anti-DDoS Advanced instance |


