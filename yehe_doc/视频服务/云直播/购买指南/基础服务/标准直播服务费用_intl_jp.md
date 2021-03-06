## 注意事項

- 課金方式：日次決済、料金後払い。
- 課金サイクル：日次決済で課金されます。毎日午前10時に前日のトラフィック料金が差し引かれます。詳細は請求書のとおりです。
>! トラフィック/帯域幅の変換単位は1000です。例えば、1TB = 1000GBとなります。
- **新規ユーザーがCSSをアクティブにすると、デフォルトでトラフィックの日次決済課金が適用されます**。
- CSSは、北京時間の00:00から23:59までを1暦日としてカウントします。


<span id="domestic"></span>
## トラフィック帯域幅
ライブストリーミングのトラフィック/帯域幅料金は、Tencent Cloud CSSの基本的な課金項目ですが、これは、CSSサービスによってCSSコンテンツを視聴するときに発生するダウンストリームのトラフィック/帯域幅の料金のことです。日次決済の料金後払いの課金方法としては、[トラフィック課金](#flow)と[帯域幅課金](#bandwidth)という2種類が提供されており、ユーザーは実際のニーズに応じてご自分に適した課金方法を選択できます。

<span id="flow"></span>
### トラフィック課金
#### 課金価格
CSSのトラフィック課金では、毎日の料金を段階的に設定する従量課金制が適用されます。日次決済トラフィック課金の段階的価格の詳細については、次の表のとおりです。

| トラフィック段階          | 価格（米ドル/GB/日） |
| ------------------------- | -------------------- |
| 0 - 500GB                 | 0.0459               |
| 500GB（500GBを含む）～2TB | 0.0441               |
| 2TB（2TBを含む）～50TB    | 0.0406               |
| 50TB（50TBを含む）～100TB | 0.0335               |
| ≧ 100TB                   | 0.0282               |

#### 課金説明
- 課金項目：CSS視聴によって発生した中国本土（大陸）におけるネットワーク全体のダウンストリームトラフィック。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日のトラフィック累計値に対応する段階の単価を乗じて算出します。
- 計算式：
  - 消費トラフィック = ビットレート / 8 × すべての人の総視聴時間。 
    
    >?すべての人の総視聴時間 = 平均オンライン人数 × 1人あたりの平均視聴時間。例えば、1人が60分間視聴した場合と60人がみな1分間視聴した場合の総時間は同じになります。
  - トラフィック料金=トラフィック消費量×その日の累計ダウンストリームトラフィックに対応する段階のGBあたりの単価。

#### 課金の例

- CSSビットレートが1Mbpsの場合（このビットレートはオーディオビットレートとビデオビットレートの合計です。トランスコーディングをオンにして特定のビットレートを設定している場合は、この設定値はビデオビットレートのみになり、オーディオビットレートを加算してトラフィックを計算する必要が出てきます）、ライブストリーミング継続時間が2時間で、そのうちライブストリーミングを1時間視聴した人数が100人、ライブストリーミングを2時間視聴した人数が50人であった場合、消費されるトラフィックはおよそ次のようになります。
  1（Mbps）/8 × 7200（s） × 50（人）+1（Mbps）/8 × 3600（s） × 100（人） = 90000（MB） = 90GB。
- 2021年1月1日にCSSサービスを利用し、90GBのダウンストリームトラフィックが発生した場合、2021年1月2日に支払うべき日次決済のライブストリーミングトラフィックの請求額は、次のようになります。
  0.0459（米ドル/GB）× 90（GB）= 4.131米ドル。

<span id="bandwidth"></span>

### 帯域幅課金

#### 課金価格

CSSの帯域幅課金では、1日の到達量による従量課金が適用され、その日のピーク帯域幅が課金値となります。日次決済のピーク帯域幅課金の段階的価格の詳細については、次の表のとおりです。

| 帯域幅段階                      | 価格（米ドル/Mbps/日） |
| ------------------------------- | ---------------------- |
| 0 - 500Mbps                     | 0.1129                 |
| 500Mbps（500Mbpsを含む）～5Gbps | 0.1094                 |
| 5Gbps（5Gbpsを含む）～20Gbps    | 0.1041                 |
| ≧ 20Gbps                        | 0.1024                 |

#### 課金説明

- 課金項目：CSS視聴で発生する中国内地（大陸）のネットワーク全体の下り帯域幅。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日の帯域幅ピーク値に対応する段階の単価を乗じて算出します。

#### 課金の例

- ライブストリーミングのビットレートが500Kbps（このビットレートは音声ビットレートとビデオビットレートの和となりますが、トランスコーディングを有効にして特定のビットレートを設定している場合、この設定値がビデオのみのビットレートとなりますので、オーディオビットレートを加えて帯域幅を計算する必要があります）、ライブストリーミング時間が1時間、視聴者数が100人となる場合、消費したおおよその帯域幅は次となります。
  500（Kbps） × 100 = 50000（Kbps） = 50Mbps。
- 2021年1月1日にCSSサービスを使用し、50Mbpsの下り帯域幅が発生した場合、2021年1月2日に支払いが必要なCSS帯域幅の請求書は次となります。
  1日あたりのライブストリーミング帯域幅の料金 = 0.1129（米ドル/Mbps/日）× 50（Mbps）= 5.645 米ドル。

>? ライブストリーミングの業務量が大量にあり、Tencent Cloudの消費量が1万米ドルを超えたか、または超えることが予想される場合、日次決済の課金方法ではお客様のニーズを満たせない恐れがあります。その場合、お客様の課金方法と価格をTencent Cloudの担当者と協議して設定することができます。[チケットを提出](https://console.cloud.tencent.com/workorder/category) して詳細をお問い合わせください。

<span id="overseas_speed"></span>

## グローバル/中国香港・中国マカオ・中国台湾のアクセラレーション

CSSのグローバル/中国香港・中国マカオ・中国台湾のトラフィックと帯域幅の統計データは、ユーザーがグローバル/中国香港・中国マカオ・中国台湾のアクセラレーションオリジンサーバーとの間で接続を確立することによって発生したダウンストリームトラフィック・帯域幅のデータです。日次決済の料金後払いの課金方法としては、[トラフィック課金](#overseas_flow)と[帯域幅課金](#overseas_bandwidth)という2種類が提供されており、新規ユーザーがCSSをアクティブにした場合、デフォルトでトラフィック課金が適用されます。
<span id="overseas_flow)"></span>

### グローバル/中国香港・中国マカオ・中国台湾のトラフィック課金

#### 課金価格

CSSのグローバル/中国香港・中国マカオ・中国台湾のトラフィック課金では、1日の到達量による従量課金が適用されます。日次決済のトラフィック課金の段階的価格の詳細については、次の表のとおりです。

| トラフィック段階          | 価格（米ドル/GB/日） |
| ------------------------- | -------------------- |
| 0 - 500GB                 | 0.0794               |
| 500GB（500GBを含む）～2TB | 0.0759               |
| 2TB（2TBを含む）～50TB    | 0.0724               |
| 50TB（50TBを含む）～100TB | 0.0671               |
| ≧ 100TB                   | 0.06                 |

#### 課金説明

- 課金項目：CSS視聴によって発生したグローバル/中国香港・中国マカオ・中国台湾におけるネットワーク全体のダウンストリームトラフィック。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日のトラフィック累計値に対応する段階の単価を乗じて算出します。

#### 課金の例

2021年1月1日にCSSグローバル/中国香港・中国マカオ・中国台湾サービスを利用し、1TBのダウンストリームトラフィックが発生した場合、2021年1月2日に支払うべきライブストリーミングトラフィックの請求額は、次のようになります。
1日あたりのライブストリーミングトラフィック料金 = 0.0759（米ドル/GB）× 1000(GB)= 75.9 米ドル。

<span id="overseas_bandwidth)"></span>

### グローバル/中国香港・中国マカオ・中国台湾の帯域幅課金

#### 課金価格

CSSグローバル/中国香港・中国マカオ・台湾の帯域幅課金には、1日に到達した階層の価格による課金を採用し、当日のグローバル/中国香港・マカオ・台湾のピーク帯域幅を課金の値とします。日ごとのピーク帯域幅課金の階層価格設定は下表のとおりです。

| 帯域幅段階                      | 価格（米ドル/Mbps/日） |
| ------------------------------- | ---------------------- |
| 0 - 500Mbps                     | 0.2294                 |
| 500Mbps（500Mbpsを含む）～5Gbps | 0.2118                 |
| ≧ 5Gbps                         | 0.1941                 |

#### 課金説明

- 課金項目：CSS視聴によって発生したグローバル/中国香港・中国マカオ・中国台湾におけるネットワーク全体のダウンストリーム帯域幅。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日の帯域幅ピーク値に対応する段階の単価を乗じて算出します。

#### 課金の例

2021年1月1日にCSSグローバル/中国香港・中国マカオ・中国台湾サービスを利用し、600Mbpsのダウンストリーム帯域幅が発生した場合、2021年1月2日に支払うべきライブストリーミング帯域幅の請求額は次のとおりです。
1日あたりのライブストリーミング帯域幅料金 = 0.2118（米ドル/Mbps）× 600(Mbps)= 127.08 米ドル
