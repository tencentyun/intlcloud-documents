

## 基本情報クラスAPI
| API名                   | API機能                    |
| ------------------------------ | ------------------------------- |
| [BGPIPGetInfo](https://cloud.tencent.com/document/product/1014/31246)             | 指定されたAnti-DDoS Advancedインスタンスの詳細情報の取得       |
| [BGPIPRename](https://cloud.tencent.com/document/product/1014/31245)                    | 指定されたAnti-DDoS Advancedインスタンス名の変更 |
| [BGPIPSetCCThreshold](https://cloud.tencent.com/document/product/1014/31244)            | 指定されたAnti-DDoS AdvancedインスタンスのCC防護しきい値の設定 |
| [BGPIPSetElasticProtectionLimit](https://cloud.tencent.com/document/product/1014/31243) | 指定されたAnti-DDoS Advancedインスタンスの弾性防護ピーク値の設定 |
|[ AddCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31242)            | 単一CCカスタムポリシーの追加          |
| [EditCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31241)           | 単一CCカスタムポリシーの編集          |
| [GetCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31240)            | 単一CCカスタムポリシー情報の取得      |
| [GetCustomCCStrategyList](https://cloud.tencent.com/document/product/1014/31239)        | CCカスタムポリシーリストの取得          |
| [RemoveCustomCCStrategy](https://cloud.tencent.com/document/product/1014/31238)         | 単一CCカスタムポリシーの削除          |
| [SetCustomCCStrategyStatus](https://cloud.tencent.com/document/product/1014/31237)      | 単一CCカスタムポリシーの有効化・無効化    |
| [OpenDomainCCProtection](https://cloud.tencent.com/document/product/1014/31236)         | ドメイン名規則CC防護の有効化            |
| [CloseDomainCCProtection](https://cloud.tencent.com/document/product/1014/31235)        | ドメイン名規則CC防護の無効化            |

## 防護情報クラスAPI
| API名                | API機能                                                    |
| ----------------------- | ----------------------------------------------------------- |
| [BGPIPDDoSGetCounter](https://cloud.tencent.com/document/product/1014/31253)     | 指定されたAnti-DDoS AdvancedインスタンスがDDoS攻撃によって攻撃された回数、ピーク値、および弾性防護の有効化回数を取得 |
| [BGPIPDDoSGetStatistics](https://cloud.tencent.com/document/product/1014/31252)  | 指定されたAnti-DDoS AdvancedインスタンスがDDoS攻撃によって攻撃されたトラフィック統計を取得                       |
| [BGPIPDDoSGetDetails](https://cloud.tencent.com/document/product/1014/31251)     | 指定されたAnti-DDoS AdvancedインスタンスがDDoS攻撃によって攻撃されたトラフィックの詳細を取得                       |
| [BGPIPCCGetCounter](https://cloud.tencent.com/document/product/1014/31250)       | 指定されたAnti-DDoS AdvancedインスタンスがCC攻撃によって攻撃された回数、ピーク値                     |
| [BGPIPCCGetStatistics](https://cloud.tencent.com/document/product/1014/31249)    | 指定されたAnti-DDoS AdvancedインスタンスがCC攻撃によって攻撃されたトラフィック統計チャートを取得                     |
| [BGPIPCCGetDetails](https://cloud.tencent.com/document/product/1014/31248)       | 指定されたAnti-DDoS AdvancedインスタンスがCC攻撃によって攻撃されたトラフィックの詳細を取得                         |
| [BGPIPTransGetStatistics](https://cloud.tencent.com/document/product/1014/31247) | 指定されたAnti-DDoS AdvancedインスタンスがTencent Cloud外部CVMに転送されたトラフィックの統計チャートを取得           |

## サービスリストクラスAPI
| API名                  | 機能説明                                  |
| ------------------------- | ----------------------------------------- |
| [BGPIPGetServicePacks](https://cloud.tencent.com/document/product/1014/31261)      | このユーザー名配下のすべてのAnti-DDoS Advancedインスタンスリストを取得 |
| [BGPIPGetServiceStatistics](https://cloud.tencent.com/document/product/1014/31262) | Anti-DDoS Advancedの過去の使用日数と防御回数を取得 |

## 転送規則クラスAPI
| API名                 | 機能説明                                  |
| ------------------------ | ----------------------------------------- |
| [BGPIPAddTransRules](https://cloud.tencent.com/document/product/1014/31270)       | 指定されたAnti-DDoS Advancedインスタンスに4層転送規則を追加    |
| [BGPIPEditTransRules](https://cloud.tencent.com/document/product/1014/31269)      | 指定されたAnti-DDoS Advancedインスタンスの指定4層転送規則を編集       |
| [BGPIPGetTransRules](https://cloud.tencent.com/document/product/1014/31268)       | 指定されたAnti-DDoS Advancedインスタンスの4層転送規則のリストを取得 |
| [BGPIPDeleteTransRules](https://cloud.tencent.com/document/product/1014/31267)    | 指定されたAnti-DDoS Advancedインスタンスの指定4層転送規則を削除         |
| [BGPIPAddWadTransRules](https://cloud.tencent.com/document/product/1014/31266)    | 指定されたAnti-DDoS Advancedインスタンスに7層転送規則を追加    |
| [BGPIPEditWadTransRules](https://cloud.tencent.com/document/product/1014/31265)   | 指定されたAnti-DDoS Advancedインスタンスの指定7層転送規則を編集             |
| [BGPIPGetWadTransRules](https://cloud.tencent.com/document/product/1014/31263)    | Anti-DDoS Advancedインスタンスの7層転送規則のリストを取得   |
| [BGPIPDeleteWadTransRules](https://cloud.tencent.com/document/product/1014/31264) | 指定されたAnti-DDoS Advancedインスタンスの指定7層転送規則を削除         |

## ホワイトリストクラスAPI
| API名         | 機能説明                                      |
| ---------------- | --------------------------------------------- |
| [GetWhiteUrl](https://cloud.tencent.com/document/product/1014/31277)      | 指定されたAnti-DDoS Advancedインスタンスのホワイトリストを取得         |
| [AddWhiteUrl](https://cloud.tencent.com/document/product/1014/31276)      | 指定されたAnti-DDoS AdvancedインスタンスにURLホワイトリストを追加     |
| [RemoveWhiteUrl](https://cloud.tencent.com/document/product/1014/31275)   | 指定されたAnti-DDoS AdvancedインスタンスのURLホワイトリストを削除  |
| [GetSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31274)    | 指定されたAnti-DDoS AdvancedインスタンスのソースIPホワイトリストを取得   |
| [AddSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31273)    | 指定されたAnti-DDoS AdvancedインスタンスにソースIPホワイトリストを追加    |
| [RemoveSrcWhiteIP](https://cloud.tencent.com/document/product/1014/31272) | 指定されたAnti-DDoS AdvancedインスタンスのソースIPホワイトリストを削除 |

## ブラックリストクラスAPI
| API名         | 機能説明                                      |
| ---------------- | --------------------------------------------- |
| [AddSrcBlackIP](https://cloud.tencent.com/document/product/1014/31278)    | 指定されたAnti-DDoS AdvancedインスタンスにソースIPブラックリストを追加    |
| [RemoveSrcBlackIP](https://cloud.tencent.com/document/product/1014/31279) | 指定されたAnti-DDoS AdvancedインスタンスのソースIPブラックリストを削除 |


