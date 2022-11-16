オーディオビデオ端末のLicenseには**CSSプッシュLicense**、**UGSV License**、**ビデオ再生License**があります。課金と購入の詳細については[価格一覧](https://www.tencentcloud.com/document/product/647/50553)をご参照ください。ご購入後は[TRTC](https://console.tencentcloud.com/trtc)、 [CSS](https://console.tencentcloud.com/live/license)または[VOD](https://console.tencentcloud.com/vod/license)のいずれかの製品のコンソールで、各Licenseの追加と更新などの操作を行うことができます。各Licenseによってロック解除される関連の機能モジュールは次のとおりです。

| オーディオビデオ端末License | 機能モジュールのロック解除            |
| -------------------- | ----------------------- |
| CSSプッシュLicense     | CSSプッシュ + ビデオ再生 |
| UGSV License       | UGSV（ライト版/標準版） + ビデオ再生 |
| ビデオ再生License | ビデオ再生 |

>! バージョン10.1からは、CSSプッシュLicenseおよびUGSV Licenseにビデオ再生Licenseのすべての機能が含まれるため、Player SDKのビデオ再生機能のロック解除にもご利用いただけます。

オーディオビデオ端末SDKのCSSプッシュLicense、UGSV License、ビデオ再生Licenseについて、**ここではCSSプッシュLicenseを例に**、オーディオビデオ端末Licenseのテスト版と正式版の追加と更新などの操作についてガイダンスを行います。

[](id:test)
## テスト版License

[](id:creat_test)
### テスト版Licenseの申請

ライブストリーミングモジュールのテスト版License（無料テスト版の有効期間は28日間です）を無料で申請し、体験することができます。


>? テスト開始申請時刻が`2022-10-1 11:34:55`であった場合、28日後の期限切れ時刻は`2022-10-28 00:00:00`となります。


モジュールのテストを申請する際、**テスト版Licenseを新規作成して機能モジュールのテストを申請する**か、または**作成済みのテストアプリケーションで新機能モジュールのテストを申請する**という2種類の方法から選択して、テスト版Licenseを作成することができます。
<dx-tabs>
::: 方法1：テスト版Licenseを新規作成して機能モジュールのテストを申請する
1. [TRTC](https://console.tencentcloud.com/trtc)、 [CSS](https://console.tencentcloud.com/live/license)または[VOD](https://console.tencentcloud.com/vod/license)のいずれかの製品のコンソールにログインし、**テスト版Licenseの新規作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/4507bd038c2a6e43cf91205383a1904f.png)
2. 実際の必要に応じて`App Name`、`Package Name`および`Bundle ID`を入力し、機能モジュールの**ライブストリーミング**（CSSプッシュ + ビデオ再生）にチェックを入れ、**OK**をクリックします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/af9ee37d5d25af0dc63221ff13cac3d6.png" style="zoom:67%;" />
1. テスト版Licenseの作成に成功すると、発行されたLicense情報が画面に表示されます。**SDKの初期化設定の際に、KeyとLicense URLという2つのパラメータを渡す必要があります。次の情報を適切に保存してください。**
![](https://qcloudimg.tencent-cloud.cn/raw/67b33614792136bb295b3f47a024291f.png)
:::
::: 方法2：作成済みのテストアプリケーションで新機能モジュールのテストを申請する
作成済みのテストアプリケーションで**CSSプッシュ**（CSSプッシュ + ビデオ再生）機能テストモジュールを申請したい場合は、次の手順で行います。
1. テストしたいアプリケーションを選択し、**新機能モジュールのテスト**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/026830658f7815b3d43432a501f2327a.png)
2. 機能モジュールの**CSSプッシュ**（CSSプッシュ + ビデオ再生）にチェックを入れ、**OK**をクリックします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/80d4dffff43aa6e299088d4a1b06db72.png" style="zoom:67%;" />
:::
</dx-tabs>

>? 
>- テスト版Licenseの有効期間内に右側の**編集**をクリックして進み、Bundle IDとPackage Name情報を変更し、**OK**をクリックして保存することができます。
>- Package NameまたはBundle Idがない場合は、「-」と入力します。
>- テスト版Licenseの有効期間は合計28日間で、**申請は一度しかできません**。引き続きご利用になりたい場合は、[正式版License](#formal)をご購入ください。

[](id:up_test)
### テスト版Licenseのアップグレード
ライブストリーミング機能モジュールのテスト版Licenseを正式版Licenseにアップグレードすると、1年間の使用有効期間が得られます。ご希望の場合は次の操作を行ってください。
1.テスト版Licenseのライブストリーミング機能モジュールの**アップグレード**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/6daf850b30a29014ab8cbd0f1a3f500f.png)
2. 機能モジュールアップグレード画面に進み、**今すぐバインド**をクリックし、バインドしたいCSSトラフィックリソースパックまたは単体のLicense（バインド可能なLicenseリソースがない場合は、[オーディオビデオ端末SDK購入ページ](https://buy.tencentcloud.com/license)で購入できます）を選択し、**OK**をクリックすると、ライブストリーミング機能モジュールの正式版Licenseにアップグレードできます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/087fb89a73fa9cffd80e0da4840783f6.png" alt="image" style="zoom: 50%;" /><img src="https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png" style="zoom:50%;" />

[](id:formal)
## 正式版License
[](id:creat_formal)
### 正式版Licenseの購入
1. 購入方法：
    - 単体の[CSSプッシュLicense](https://www.tencentcloud.com/document/product/647/50553)を[**購入**](https://buy.tencentcloud.com/license)し、使用の権限を取得します（権限の有効期間は、パッケージ名のバインド日から起算して1年後の期間満了翌日の00:00:00までです）。
2. ライブストリーミング正式版Licenseをバインドします。**正式なアプリケーションを新規作成してLicenseをバインドする**か、または**作成済みのアプリケーションでライブストリーミング正式版モジュールのロックを解除し、Licenseをバインドする**という2種類の方法から選択して正式版Licenseのバインドを行うことができます。
<dx-tabs>
::: 方法1：正式なアプリケーションを新規作成してLicenseをバインドする
1. [TRTC](https://console.tencentcloud.com/trtc)、 [CSS](https://console.tencentcloud.com/live/license)または[VOD](https://console.tencentcloud.com/vod/license)のいずれかの製品のコンソールのLicense管理に進み、**正式版Licenseの新規作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/c7689b0f319f616a5e5e3ecf47267b65.png)
2. 正式アプリケーションの`App Name`、`Package Name`および`Bundle ID`情報を入力し、機能モジュールの**ライブストリーミング**（CSSプッシュ + ビデオ再生）にチェックを入れ、**次のステップ**をクリックします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0ba8765431755c7807787782a157297.png" style="zoom:67%;" />
3 リソース項目選択およびLicenseバインド画面に進み、**今すぐバインド**をクリックし、**未バインド**のライブストリーミングトラフィックリソースパックまたは単体のLicense（バインド可能なLicenseリソースがない場合は、[オーディオビデオ端末SDK購入ページ](https://buy.tencentcloud.com/license)で購入できます）を選択し、**OK**をクリックすると、アプリケーションを作成して正式版Licenseを発行できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ddb304e3d9e35959c0ba93a4138189a.png" style="zoom:50%;" />

>? **OK**をクリックする前に、Bundle IDとPackage Nameが業務で使用しているパッケージ名の情報と一致しているかを再度確認する必要があります。ストアに送信したものと一致しない場合は、送信前に変更してください。 **正式版Licenseは一度送信に成功すると、License情報の変更ができなくなります**。

4. 正式版Licenseの作成に成功すると、発行された正式版License情報が画面に表示されます。SDKの初期化設定の際に、KeyとLicense URLという2つのパラメータを渡す必要があります。次の情報を適切に保存してください。
![](https://qcloudimg.tencent-cloud.cn/raw/11fcae56bf1fcad8641ba789bdaaa517.png)
:::
::: 方法2：作成済みの公式アプリケーションでモジュールのロックを解除する
1. 追加したい**CSSプッシュ**（CSSプッシュ + ビデオ再生）機能モジュールの正式アプリケーションを選択し、**新機能モジュールのロックを解除**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/e1ab736ce2f80e74214dbca9a47f10fd.png)
1. **CSSプッシュ**（CSSプッシュ + ビデオ再生）を選択し、**次のステップ**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png)
1. リソース項目選択およびLicenseバインド画面に進み、**今すぐバインド**をクリックし、**未バインド**のライブストリーミングトラフィックリソースパックまたは単体のLicense（バインド可能なLicenseリソースがない場合は、[オーディオビデオ端末SDK購入ページ](https://buy.tencentcloud.com/license)で購入できます）を選択し、**OK**をクリックすると、アプリケーションに正式版ライブストリーミング機能モジュールを生成することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/095e35fc6947c3399ca30d66d019b2f5.png)
:::
</dx-tabs>

[](id:update_formal)
### 正式版Licenseの有効期間更新
[TRTC](https://console.tencentcloud.com/trtc)、 [CSS](https://console.tencentcloud.com/live/license)または[VOD](https://console.tencentcloud.com/vod/license)のいずれかの製品のコンソールにログインし、License管理ページでライブストリーミング正式版Licenseの有効期間を確認できます。もしくは、[メッセージサブスクリプション](https://console.cloud.tencent.com/message/subscription)でオーディオビデオ端末SDKをサブスクライブし、**サイト内メッセージ**/**メール**/**SMS**/**WeChat**/**WeCom**などのメッセージ受信チャネルによって、正式版Licenseの期限通知を受け取ることができます。CSSプッシュ正式版Licenseの期限通知は期限切れの30日前、15日前、7日前、1日前に1回ずつ送信され、業務の正常な実行に影響が出ないように速やかに更新するようリマインドします。CSSプッシュ正式版Licenseがすでに期限切れの場合は、次の操作によって更新することができます。
1. 有効期間を更新したいLicenseを選択し、ライブストリーミング機能モジュール内の**有効期間の更新**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/534f5d02cb72a6950ad5d37fb3666c70.png)
2. **今すぐバインド**をクリックし、**未バインド**のライブストリーミングトラフィックリソースパックまたは単体のLicense（バインド可能なLicenseリソースがない場合は、[オーディオビデオ端末SDK購入ページ](https://buy.tencentcloud.com/license)で購入できます）を選択し、**OK**をクリックします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b1f279e5cd439386147c4f4aa96d852.png" style="zoom:50%;" />
3. 更新後の有効期限の状況を確認します。

>! **正式版CSSプッシュLicenseは情報の変更をサポートしていません**。License情報を変更する必要がある場合は、リソースパックを購入後、Licenseの有効期間の更新は行わず、**Licenseの追加**をクリックしてLicenseを再追加し、新しいパッケージ名情報をバインドしてください。