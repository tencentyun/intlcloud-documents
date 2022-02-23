
一般のユーザーがネットワーク品質を評価することは困難ですので、ビデオ通話を行う前にネットワークテストを実行することをお勧めします。速度測定はネットワーク品質をより直感的に評価することができます。

## 注意事項

- 通話品質への影響を避けるため、ビデオ通話中にテストしないでください。
- 速度測定は一定量のトラフィックを消費するため、ごくわずかな追加的トラフィック費用が発生します（ほぼ無視できる程度です）。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows | Electron | Web端末|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003;    | &#10003;（参考：[Web端末チュートリアル](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html)） |

## 速度測定の原理

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- 速度測定の原理は次のとおりです。SDKが検出パケットのバッチをサーバーノードに送信した後、返送されたパケットの品質を集計し、コールバックインターフェースを介して速度測定の結果を通知します。
- 速度測定の結果は、SDKの次のサーバー選択戦略を最適化するために使用されます。したがって、ユーザーが最初の通話を行う前に速度測定を実行することを推奨します。このことは最適なサーバーの選択に役立ちます。 また極めて不満足なテスト結果であった場合は、目立つUIを使用し、より適切なネットワークを選択するよう、ユーザーに促すことができます。
- 速度測定の結果（[TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult)）には、次のいくつかのフィールドが含まれます。
<table>
<tr><th>フィールド</th><th>意味</th><th>意味の説明</th>
</tr><tr>
<td>success</td>
<td>成功したかどうか</td>
<td>今回のテストが成功したかどうか</td>
</tr><tr>
<td>errMsg</td>
<td>エラー情報</td>
<td>帯域幅テストの詳細なエラー情報</td>
</tr><tr>
<td>ip</td>
<td>サーバー</td>
<td>サーバー速度測定のIP</td>
</tr><tr>
<td><a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga25f9ccb045890cb18a5f647ef3c1f974">quality</a></td>
<td>ネットワーク品質スコア</td>
<td>評価アルゴリズムによって測定および計算されたネットワーク品質。lossが低いほど、rttが小さいほど、スコアは高くなります</td>
</tr><tr>
<td>upLostRate</td>
<td>上りパケット損失率</td>
<td>範囲は[0 - 1.0]、例えば0.3はサーバーに送信される10データパケットごとに、途中で3パケットが失われる可能性があることを意味します</td>
</tr><tr>
<td>downLostRate</td>
<td>下りパケット損失率</td>
<td>範囲は[0 - 1.0]、例えば0.2はサーバーから受信する10データパケットごとに、途中で2パケットが失われる可能性があることを意味します</td>
</tr><tr>
<td>rtt</td>
<td>ネットワーク遅延</td>
<td>SDKとサーバー間の往復で消費される時間を表します。値が小さいほど遅延が少なく、通常の値は10msから100msの間です</td>
</tr><tr>
<td>availableUpBandwidth</td>
<td>上り帯域幅</td>
<td>予測される上り帯域幅。単位はkbps、 -1は無効値を表わします</td>
</tr><tr>
<td>availableDownBandwidth</td>
<td>下り帯域幅</td>
<td>予測される下り帯域幅。単位はkbps。 -1は無効値を表わします</td>
</tr></table>

## 速度測定方法

TRTCCloudの`startSpeedTest`機能によって速度測定機能を起動できます。速度測定の結果はコールバック関数によって返されます。

<dx-codeblock>
::: Objective-C ObjectiveC
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    TRTCSpeedTestParams *params;
    // sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    params.sdkAppID = sdkAppId;
    params.userID = userId;
    params.userSig = userSig;
    // 予想される上り帯域幅（kbps、値範囲： 10 ～ 5000、0の時はテストなし）
    params.expectedUpBandwidth = 5000;
    // 予想される下り帯域幅（kbps、値範囲： 10 ～ 5000、0の時はテストなし）
    params.expectedDownBandwidth = 5000;
    [trtcCloud startSpeedTest:params];
}
- (void)onSpeedTestResult:(TRTCSpeedTestResult *)result {
    // 速度測定完了後、測定結果がコールバックされます
}
:::
::: Java Java
//ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
public void onLogin(String userId, String userSig) 
{
  TRTCCloudDef.TRTCSpeedTestParams params = new TRTCCloudDef.TRTCSpeedTestParams();
  params.sdkAppId = GenerateTestUserSig.SDKAPPID;
  params.userId = mEtUserId.getText().toString();
  params.userSig = GenerateTestUserSig.genTestUserSig(params.userId);
  params.expectedUpBandwidth = Integer.parseInt(expectUpBandwidthStr);
  params.expectedDownBandwidth = Integer.parseInt(expectDownBandwidthStr);
	// sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    trtcCloud.startSpeedTest(params);
}

// 速度測定の結果を監視し、TRTCCloudListenerを継承し、次のメソッドを実装します
void onSpeedTestResult(TRTCCloudDef.TRTCSpeedTestResult result)
{
    // 速度測定完了後、測定結果がコールバックされます
}
:::
::: C++ C++
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
void onLogin(const char* userId, const char* userSig)
{
    TRTCSpeedTestParams params;
    // sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    params.sdkAppID = sdkAppId;
    params.userId   = userid;
    param.userSig = userSig;
    // 予想される上り帯域幅（kbps、値範囲： 10 ～ 5000、0の時はテストなし）
    param.expectedUpBandwidth = 5000;
    // 予想される下り帯域幅（kbps、値範囲： 10 ～ 5000、0の時はテストなし）
    param.expectedDownBandwidth = 5000;
    trtcCloud->startSpeedTest(params);
}

// 速度測定結果を監視します
void TRTCCloudCallbackImpl::onSpeedTestResult(
             const TRTCSpeedTestResult& result)
{
    // 速度測定完了後、測定結果がコールバックされます
}
:::
::: C# C#
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
private void onLogin(string userId, string userSig)
{
    TRTCSpeedTestParams params;
    // sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    params.sdkAppID = sdkAppId;
    params.userId   = userid;
    param.userSig = userSig;
    // 予想される上り帯域幅（kbps、値範囲： 10 ～ 5000、0の時はテストなし）
    param.expectedUpBandwidth = 5000;
    // 予想される下り帯域幅（kbps、値範囲： 10 ～ 5000、0の時はテストなし）
    param.expectedDownBandwidth = 5000;
    mTRTCCloud.startSpeedTest(params);
}

// 速度測定結果を監視します
public void onSpeedTestResult(TRTCSpeedTestResult result)
{
    // 速度測定完了後、測定結果がコールバックされます
}
:::
</dx-codeblock>

## 速度測定ツール
インターフェースを呼び出すことによるネットワーク速度測定を行いたくない場合、詳細なネットワーク品質情報を迅速に得るために、TRTCはデスクトップ版のネットワーク速度測定ツールプログラムも提供しています。
### ダウンロードリンク
[Mac](https://liteav.sdk.qcloud.com/customer/%E6%B5%8B%E8%AF%95/%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7/trtc-network-tools-latest.dmg) |[Windows](https://liteav.sdk.qcloud.com/customer/%E6%B5%8B%E8%AF%95/%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7/trtc-network-tools_Setup_latest.exe)
### テスト指標

| インジケータ         | 意味                                                                                                               |
|--------------|--------------------------------------------------------------------------------------------------------------------|
| WiFi Quality | Wi-Fi 信号品質                                                                                                  |
| DNS RTT      | Tencent Cloudのドメイン名解析時間の速度測定                                                                          |
| MTR          | MTRはネットワークテストツールで、クライアントからTRTCノードまでのパケット損失率とレイテンシーを検出することができます。また、ルートの各ジャンプに関する具体的な情報も確認できます |
| UDP Loss     | クライアントからTRTCノードまでのUDPパケット損失率                                                                                        |
| UDP RTT      | クライアントからTRTCノードまでのUDPレイテンシー                                                                                        |
| Local RTT    | クライアントからローカルゲートウェイまでのレイテンシー                                                                                        |
| Upload       | 推定上り帯域幅                                                                                                       |
| Download     | 推定下り帯域幅                                                                                                      |


### ツールスクリーンキャプチャ

クイックテスト：
![](https://qcloudimg.tencent-cloud.cn/raw/e1d7e4b4bfcd1c7c3916e56095b8ba24.png)
継続的テスト：
![](https://qcloudimg.tencent-cloud.cn/raw/76e0e62a6ea6f92779f37bd7331d0085.png)


