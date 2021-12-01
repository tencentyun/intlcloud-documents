UGSV SDK Licenseは、UGSV SDKの使用権限をアクティブ化するために用いられます。ユーザーは、コンソールでテスト版UGSV Licenseの申請または更新や表示などの操作ができます。UGSV SDKの機能に関する詳細については、[UGSV](https://intl.cloud.tencent.com/document/product/1069/37914)をご参照ください。
## テスト版Licenseの申請
テスト版Licenseを申請すると、さまざまな機能を無料で体験することができます。その使用権限は、正式版UGSV SDK Licenseのベーシック版に対応しています。初回申請時の試用期間は14日間で、1回無料で更新でき、計28日間試用できます。申請手順は次のとおりです。

### 手順1：テスト版Licenseの作成
1. [VODコンソール](https://console.cloud.tencent.com/vod/license)に進み、管理者アカウントで左側メニューから【[UGSV SDK License](https://console.cloud.tencent.com/vod/license/video)】を選択します。

2. 右上隅の【編集】をクリックし、App Name、Package NameおよびBundle IDを入力してください。

3. 【確定】をクリックすれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/5453b61401859a2599bab6ffcedbf808.png)

### 手順2：テスト版Licenseの保存
無料テスト版Licenseの作成に成功すると、発行されたLicense情報が画面に表示されます。SDKの初期化を設定するときに、KeyとLicenseUrlという2つのパラメータを渡す必要があります。次の情報を適切に保存してください。
![](https://qcloudimg.tencent-cloud.cn/raw/1500204df3029e9bbb23aa7161ad94bd.png)

## テスト版Licenseの更新
テスト版Licenseの有効期間は、[VODコンソール](https://console.cloud.tencent.com/vod/license)で確認できます。テスト版Licenseのトータルの有効期間は28日間です。14日間の初回試用時のテスト版Licenseの有効期限が近づいたら、1回更新する必要があります。手順は次のとおりです。
### 手順1：License更新の申請
【[UGSV SDK License](https://console.cloud.tencent.com/vod/license/video)】ページに進み、試用版Licenseエリアで、右上隅の【更新】をクリックします。

### 手順2：License更新の完了
更新が成功したことを示すポップアップが表示されると、右上隅の【更新】が消え、14日間の試用版Licenseの更新操作が完了します。


## テスト版Licenseの表示
License設定が成功してから一定時間経つと（ネットワークの状況に応じて異なります）、以下の方法を呼び出してLicense情報を確認することができます。

- iOS:
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- Android:
```
TXUGCBase.getInstance().getLicenceInfo(context);
```

## Licenseの使用方法
SDKに関連するインターフェースを呼び出す前に、以下に示す方法を呼び出してLicenseの設定を実行します。

- iOSでは`[AppDelegate application:didFinishLaunchingWithOptions:]`内に以下を追加することをお勧めします。
```
[TXUGCBase setLicenceURL:LicenceUrl key:Key];
```
- Androidではapplication内に以下を追加することをお勧めします。
```
TXUGCBase.getInstance().setLicence(context, LicenceUrl, Key);
```
