このドキュメントでは主に、開発者が最も関心を寄せている、オーディオビデオの品質、レイテンシー、スムーズさ、安定性、CPU、メモリ、電力消費量および発熱といった主な指標に焦点を当てています。**通常のネットワーク環境**、**脆弱なネットワーク環境**および**さまざまなリアルタイムのインタラクティブシーン（1v1、1vNなど）で、客観テストと分析の総括を行います。

## ロスレスで脆弱なネットワーク環境での効果の品質

### テストシーン

ビデオ通話とオンラインライブストリーミングのオーディオビデオシーンと音声通話シーン

### パラメータ設定
- **ビデオ通話：**
<table><tr><th>パラメータタイプ</th><th>設定情報</th></tr>
<tr><td>解像度</td><td>368 × 640</td></tr>
<tr><td>ビットレート</td><td>400Kbps</td>
</tr><tr>
<td>フレームレート</td><td>15</td>
</tr></table>
- **インタラクティブライブストリーミング：**
<table><tr><th>パラメータタイプ</th><th>設定情報</th></tr>
<tr><td>解像度</td><td>720 × 1280</td></tr>
<tr>
<td>ビットレート</td><td>1200Kbps</td>
</tr><tr>
<td>フレームレート</td><td>15</td>
</tr></table>



### 極限ネットワーク耐性テストデータ
極限ネットワーク耐性テストとは、SDKがさまざまなネットワーク障害環境において耐えられる最大のネットワーク障害をテストすることをいいます。
![](https://main.qcloudimg.com/raw/d71b4a2b2ff2af3a1bd5309f40355131.png)

### オーディオ脆弱ネットワークMOS値
データの解読：Tencent Real-Time Communication （TRTC）は、非常に理想的ではないネットワーク環境で、より低いレイテンシーでより高い音質を保証します。
次は、以下の脆弱なットワーク環境におけるTRTCの客観的なMOS評価結果です。
![](https://main.qcloudimg.com/raw/250562e60b4af3035a1b90ade8a9d7af.png)



## クライアントSDK性能データ

### テストデバイス情報
|  デバイスタイプ  |  プロセッサタイプ |   メモリ  |
| ------------ | ----------- | ---- |
| Androidデバイス1 | Snapdragon835-8コア| | 6G   |
| Androidデバイス2 | Kirin980-8コア| 8G   |
| iOSデバイス1     | A8-デュアルコア     | 3G   |
| iOSデバイス2     | A13-6コア     | 4G   |

## テストパラメータ設定

| パラメータタイプ | 設定情報 |
| ------ | ------- |
| 解像度 | 240 × 320 |
| ビットレート   | 100kbps |
| フレームレート   | 15      |

### テストプランの説明

- **テストシーン**：1v1、1v2、1v3、1v4、1v8。
- **テスト時間**：各シーンで30分間テストされます。
- **テストプラン**：Linuxプッシュロボットを使用して他人数のシーンを作成し、各テストデバイスを個別にテストします。

### テスト結果

データの解読：TRTC SDKは、CPU使用率、メモリ使用量、発熱および電力消費量など、さまざまな性能において優れたパフォーマンスを発揮します。少ないハードウェアリソースで、高品質のオーディオビデオサービスを提供することができます。

- **App CPU使用率：**
![](https://main.qcloudimg.com/raw/9c6a43b9ad52982575267f0d30ecb9e7.png)
- **Appメモリ使用率：**
![](https://main.qcloudimg.com/raw/980eed9bacc5add39a2a74e8cf534ca7.png)
-**システムの合計CPU使用率：**
![](https://main.qcloudimg.com/raw/55e9dee9a79cb0a565279471d6ce9df2.png)
-**システムの合計メモリ使用率：**
![](https://main.qcloudimg.com/raw/227236da4935eb07cbcb490684f02a54.png)
- **稼働30分間の電力消費量：**
![](https://main.qcloudimg.com/raw/c973dfcca4888e10b5e9d171732c6395.png)
- **稼働30分間の発熱量の増分：**
![](https://main.qcloudimg.com/raw/85df93deb059759ab9548416e0c2cc3b.png)


## 付録1：オーディオビデオ品質指標の説明

<table>
<tr><th width="17%">品質指標</th><th width="50%">説明</th><th>事例</th>
</tr><tr>
<td>Loss</td>
<td>Networkingパケット損失</td>
<td>50% Lossとは、10パケットのうち5パケットが失われることを意味します</td>
</tr><tr>
<td>RTT</td>
<td>レイテンシーを意味します</td>
<td>200 RTTはSDKによって送信されるパッケージであり、200ms後にネットワークから送信されます</td>
</tr><tr>
<td>Jitter</td>
<td>ジッターを意味します</td>
<td>300 JitterはSDKが送信するパッケージです。ランダムな確率で20ms、280ms、50ms、250msなど遅延する可能性があります。最大レイテンシーは300ms、平均レイテンシーは150msです</td>
</tr><tr>
<td>MOS値</td>
<td>通常、通信システムの音声品質を測定するための重要な指標として用いられます。客観的なMOS値は、Spirent Nomadデバイスを採用してPOLQAのスコアリングを行います。スコアが高いほど、音質が良いことを意味します</td>
<td>-</td>
</tr><tr>
<td>エンドツーエンドの遅延</td>
<td>エンドツーエンドの遅延とは、送信側での音声収集から受信側での再生までの時間をいいます</td>
<td>-</td>
</tr><tr>
<td>極限オーディオビデオ耐性テスト基準</td>
<td>ネットワークの障害を追加した後、Spirent Nomadデバイスを使用して、<a href="#POLQA">POLQA</a>をスコアリングし、foremanビデオシーケンスを使用して受信側のフレーム間隔状況を検出します。10分以上観察を続け、30個のデータポイントを取得します。<strong>3分間に3回以上の主観的に知覚できる効果の異常</strong>または<strong>1回の長時間の使用不可</strong>といった現象がある場合、耐性能力を超えているとみなします</td>
<td>-</td>
</tr></table>

>! POLQA（知覚的客観的聴取品質評価）基準。国際規格ITU-T P.863に基づいてスコアリングを行い、人間の音声評価に使用します。POLQAとは、さまざまなネットワークシーン向けのグローバルな音声品質分析基準です。[](id:POLQA)
 


## 付録2：SDK性能指標の説明

<table>
<tr><th width="16%">指標タイプ</th><th colspan=2>説明</th>
</tr><tr>
<td rowspan=2>App CPU使用率</td>
<td>Android</td>
<td>App CPUは、プロセスが標準化されていないCPU使用率を表し、統計結果はAndroid StudioProfilerと一致します。</td>
</tr><tr>
<td>iOS</td>
<td>App CPUはプロセスのCPU使用率を表し、統計結果はXcodeと一致します。<br><code>PerfDog使用率 = Xcode使用率 / コア数</code>。</td>
</tr><tr>
<td rowspan=2>システムCPU使用率</td>
<td>Android</td>
<td>Total CPUは、マシン全体が標準化されていないCPU使用率を表し、統計結果はAndroid StudioProfilerと一致します。</td>
</tr><tr>
<td>iOS</td>
<td>Total CPUはマシン全体のCPU使用率を表し、統計結果はXcodeと一致します。<br><code>PerfDog使用率 = Xcode使用率 / コア数</code>。</td>
</tr><tr>
<td rowspan=2>メモリ使用率</td>
<td>Android</td>
<td>PSS Memory、統計結果はAndroid Java API基準の結果と一致し、Meminfoとも一致します。</td>
</tr><tr>
<td>iOS</td>
<td>Xcode Memory、XCode Debug gauges統計方法。</td>
</tr><tr>
<td>電力消費量</td>
<td colspan=2>テスト中に監視電力が100%から99%に低下すると記録を開始し、終了電力値が設定され、その比率に基づいて30分間の電力消費量が算出されます。</td>
</tr><tr>
<td>発熱量の増分</td>
<td colspan=2>Appが起動していない場合は、ガンタイプ温度計を使用して現在の温度を測り、アプリを起動して各シーン、30分間実行します。<br><code>発熱量の増分=30分後の温度 - アプリが起動していないときの温度</code>。</td>
</tr></table>
