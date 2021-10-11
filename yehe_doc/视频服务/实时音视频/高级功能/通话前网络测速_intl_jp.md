一般のユーザーがネットワーク品質を評価することは困難ですので、ビデオ通話を行う前にネットワークテストを実行することをお勧めします。速度測定はネットワーク品質をより直感的に評価することができます。

## 注意事項

- 通話品質への影響を避けるため、ビデオ通話中にテストしないでください。
- 速度測定は一定量のトラフィックを消費するため、ごくわずかな追加的トラフィック費用が発生します（ほぼ無視できる程度です）。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows | Electron| Web端末|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003; | &#10003; 参考：[Web端末チュートリアル](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)  |

## 速度測定の原理

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- 速度測定の原理は次のとおりです。SDKが検出パケットのバッチをサーバーノードに送信した後、返送されたパケットの品質を集計し、コールバックインターフェースを介して速度測定の結果を通知します。
- 速度測定の結果は、SDKの次のサーバー選択戦略を最適化するために使用されます。したがって、ユーザーが最初の通話を行う前に速度測定を実行することを推奨します。このことは最適なサーバーの選択に役立ちます。 また極めて不満足なテスト結果であった場合は、目立つUIを使用し、より適切なネットワークを選択するよう、ユーザーに促すことができます。
- SDKが同時に接続可能なクラウドサーバーは、通常、3個以上のノードを持ち、測定プロセスは一台ずつ直列的に実施されることから、速度測定結果の戻り値は複数回のコールバックに分かれて通知されます。
- 速度測定の結果（[TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult)）には、次のいくつかのフィールドが含まれます。
<table>
<tr><th>フィールド</th><th>意味</th><th>意味の説明</th>
</tr><tr>
<td>ip</td>
<td>サーバー</td>
<td>速度測定結果は、毎回、対応する異なるIPアドレスに複数回コールバックされます</td>
</tr><tr>
<td>quality</td>
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
</tr></table>

## 速度測定方法

TRTCCloudの`startSpeedTest`機能を介して速度測定機能を起動することができ、速度測定の結果はコールバック関数を介して1～2秒ごとに一度コールバックされます。毎回のコールバックには SDKから1つのクラウドサーバーノードまでの速度測定結果が含まれ、コールバック回数は、SDKが全部で何台のクラウドサーバーにアクセスしたかによって異なります。


<dx-codeblock>
::: Objective-C Objective-C
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    // sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    [trtcCloud startSpeedTest:SDKAppID
                       userId:userId
                      userSig:userSig
                   completion:^(TRTCSpeedTestResult *result, NSInteger completedCount, NSInteger totalCount) {
                       NSLog(@"速度測定(第%d回/計%d回) %@", (int)completedCount, (int)totalCount, result);
                   }];
}
:::
::: Java Java
//ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
public void onLogin(String userId, String userSig) 
{
	// sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    trtcCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 速度測定の結果を監視し、TRTCCloudListenerを継承し、次のメソッドを実装します
void onSpeedTest(TRTCCloudDef.TRTCSpeedTestResult currentResult, int finishedCount, int totalCount)
{
    // SDKは複数のサーバーIPの速度測定を行い、毎回、1つのIPの速度測定結果をコールバックします
}
:::
::: C++ C++
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
void onLogin(const char* userId, const char* userSig)
{
    // sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    trtcCloud->startSpeedTest(sdkAppID, userId, userSig);
}

// 速度測定結果を監視します
void TRTCCloudCallbackImpl::onSpeedTest(
             const TRTCSpeedTestResult& currentResult, uint32_t finishedCount, uint32_t totalCount)
{
    // SDKは複数のサーバーIPの速度測定を行い、毎回、1つのIPの速度測定結果をコールバックします
}
:::
::: C# C#
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
private void onLogin(string userId, string userSig)
{
    // sdkAppIDはコンソールから取得した実際のアプリケーションのAppIDです
    mTRTCCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 速度測定結果を監視します
public void onSpeedTest(TRTCSpeedTestResult currentResult, uint finishedCount, uint totalCount)
{
    // SDKは複数のサーバーIPの速度測定を行い、毎回、1つのIPの速度測定結果をコールバックします
}
:::
</dx-codeblock>



