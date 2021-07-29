一般のユーザーがネットワーク品質を評価することは困難ですので、ビデオ通話を行う前にネットワークテストを実行することをお勧めします。速度測定はネットワーク品質をより直感的に評価することができます。

## 注意事項

- 通話品質への影響を避けるため、ビデオ通話中にテストしないでください。
- 速度測定は一定量のトラフィックを消費するため、ごくわずかな追加的トラフィック費用が発生します（ほぼ無視できる程度です）。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows | Electron | web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003;   | &#10003;  |

## 速度測定の原理

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- 速度測定の原理は次のとおりです。SDKが検出パケットのバッチをサーバーノードに送信した後、返送されたパケットの品質を集計し、コールバックインターフェースを介して速度測定の結果を通知します。

- 速度測定の結果は、SDKの次のサーバー選択戦略を最適化するために使用されます。したがって、ユーザーが最初の通話を行う前に速度測定を実行することを推奨します。このことは最適なサーバーの選択に役立ちます。 また極めて不満足なテスト結果であった場合は、目立つUIを使用し、より適切なネットワークを選択するよう、ユーザーに促すことができます。

- SDKが同時に接続可能なクラウドサーバーは、通常、3個以上のノードを持ち、測定プロセスは一台ずつ直列的に実施されることから、速度測定結果の戻り値は複数回のコールバックに分かれて通知されます。

- 速度測定の結果（`TRTCSpeedTestResult`）には、次のいくつかのフィールドが含まれます。

| フィールド | 意味|   意味の説明|
|:-------:|:-------:| :----------|
| ip | サーバーIP | 速度測定結果は、毎回、対応する異なるIP アドレスに複数回コールバックされます |
| quality | ネットワーク品質スコア | 評価アルゴリズムによって測定および計算されたネットワーク品質。lossが低いほど、rttが小さいほど、スコアは高くなります |
| upLostRate | 上りパケット損失率 |  範囲は[0 - 1.0]、例えば0.3はサーバーに送信される10パケットごとに、途中で3パケットが失われる可能性があることを意味します |
| upLostRate | 下りパケット損失率 |  範囲は[0 - 1.0]、例えば0.2はサーバーから受信する10パケットごとに、途中で2パケットが失われる可能性があることを意味します |
| rtt | ネットワーク遅延| SDKとサーバー間の往復で消費される時間を表します。値が小さいほど遅延が少なく、通常の値は10msから100msの間です|

## 速度測定方法

TRTCCloud の `startSpeedTest` 機能を介して速度測定機能を起動することができ、速度測定の結果はコールバック関数を介して1～2秒ごとに一度コールバックされます。毎回のコールバックには SDKから1つのクラウドサーバーノードまでの速度測定結果が含まれ、コールバック回数は、SDK が全部で何台のクラウドサーバーにアクセスしたかによって異なります。

- **Objective-C**

``` Objective-C
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    // sdkAppID はコンソールから取得した実際のアプリケーションの AppIDです。
    [trtcCloud startSpeedTest:SDKAppID
                       userId:userId
                      userSig:userSig
                   completion:^(TRTCSpeedTestResult *result, NSInteger completedCount, NSInteger totalCount) {
                       NSLog(@"速度測定(第%d回/計%d回) %@", (int)completedCount, (int)totalCount, result);
                   }];
}
```

- **Java**

``` java
//ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
public void onLogin(String userId, String userSig) 
{
	// sdkAppID はコンソールから取得した実際のアプリケーションの AppIDです。
    trtcCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 速度測定の結果を監視し、TRTCCloudListener を継承し、次のメソッドを実装します
void onSpeedTest(TRTCCloudDef.TRTCSpeedTestResult currentResult, int finishedCount, int totalCount)
{
    // SDK は複数のサーバー IPの速度測定を行い、毎回、1つのIPの速度測定結果をコールバックします
}
```

- **C++**

``` C++
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
void onLogin(const char* userId, const char* userSig)
{
    // sdkAppID はコンソールから取得した実際のアプリケーションの AppIDです。
    trtcCloud->startSpeedTest(sdkAppID, userId, userSig);
}

// 速度測定結果を監視します
void TRTCCloudCallbackImpl::onSpeedTest(
             const TRTCSpeedTestResult& currentResult, uint32_t finishedCount, uint32_t totalCount)
{
    // SDK は複数のサーバー IPの速度測定を行い、毎回、1つのIPの速度測定結果をコールバックします
}
```

* **C#**

```c#
// ネットワーク速度測定を起動するためのサンプルコードとして、sdkAppIdとUserSigが必要です（取得方法については基本機能をご参照ください）。
// ここではログイン後の測定開始を例示します
private void onLogin(string userId, string userSig)
{
    // sdkAppID はコンソールから取得した実際のアプリケーションの AppIDです。
    mTRTCCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 速度測定結果を監視します
public void onSpeedTest(TRTCSpeedTestResult currentResult, uint finishedCount, uint totalCount)
{
    // SDK は複数のサーバー IPの速度測定を行い、毎回、1つのIPの速度測定結果をコールバックします
}
```




