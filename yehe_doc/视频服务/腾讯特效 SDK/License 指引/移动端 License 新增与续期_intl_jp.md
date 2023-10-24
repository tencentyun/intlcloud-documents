Tencent Effect Licenseは美顔エフェクトに関連する機能をご提供します。Tencent Effect SDKパッケージまたはアトミック機能を購入すると1年間の使用権限を取得でき、対応するTencent Effectの機能のロックを解除することができます。課金と購入の詳細については、[価格一覧](https://www.tencentcloud.com/document/product/1143/45371)をご参照ください。

ご購入後に[Tencent Effectコンソール](https://console.tencentcloud.com/xmagic)でTencent Effect Licenseの追加および更新などの操作を行うことができます。
ここでは、Tencent Effectモバイル端末Licenseのテスト版と正式版の追加と更新などの操作についてガイダンスを行います。

[](id:test)
## テスト版License

### テスト版Licenseの申請[](id:create_test)

Tencent Effectモジュールのテスト版License（無料テスト版の有効期間は14日間です。1回に限り継続可能で、計28日間となります）を無料で申請し、体験することができます。
テスト版Licenseはご自身のニーズに応じた機能を選んで申請できます。美顔エフェクトについてはパッケージとアトミック機能のテスト申請が可能です。このうちパッケージでは最上級バージョンのS1 - 04の権限発行のみサポートしており、このバージョンではTencent Effect SDKパッケージのすべての機能を試すことができます。最上級バージョンS1 - 04の機能については、[機能説明](https://www.tencentcloud.com/document/product/1143/45376)をご参照ください。パッケージS1-04にはX1-01人物画像分割機能が含まれており、その他の機能は含まれません。

>! **Tencent Effectの機能モジュールは申請後、審査を経てからでなければ権限が発行されません**。テスト版の有効期限は審査によって承認された時刻を基準に算出します。試用期間終了後にテスト継続の申請を行う場合、継続期間の有効期限はテスト継続の申請を行った時刻を基準に算出します。
>- Tencent Effect機能モジュールテスト版の審査情報を送信すると**ステータスが審査中**となります。審査にかかる時間は通常1～2業務日です。審査情報送信日時が`2022-05-24 12:47:33（UTC+8）`、審査承認日時が`2022-05-24 15:23:46（UTC+8）`の場合、開始日時は`2022-05-24 15:23:46（UTC+8）`、14日後の有効期限は`2022-06-09 00:00:00（UTC+8）`となります。
>- 無料で1回継続する際、14日間の試用期間内に継続を申請した場合、有効期限は`2022-06-23 00:00:00（UTC+8）`となります。14日間の試用期間終了後に継続を申請した場合、継続の申請時刻が`2022-08-06 22:26:20（UTC+8）`であれば、継続の有効期限は`2022-08-22 00:00:00（UTC+8）`となります。

モジュールのテストを申請します。**テスト版Licenseを新規作成して機能モジュールのテストを申請する**か、または**作成済みのテストアプリケーションで新機能モジュールのテストを申請する**という2種類の方法から選択して、テスト版Licenseを作成することができます。
<dx-tabs>
::: 方法1：テスト版Licenseを新規作成して機能モジュールのテストを申請する

1. [**Tencent Effect SDKコンソール > モバイル端末License**](https://console.tencentcloud.com/xmagic)にログインし、**テスト版Licenseの新規作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/54ac63cd985f1170b2d74eaac4d0cd1d.png)
2. 実際の必要性に応じて`App Name`、`Package Name`、`Bundle ID`を入力し、テストしたい機能である**ハイグレードパッケージS1 - 04**、**アトミック機能X1-01**、**アトミック機能X1-02**を選択し、チェックを入れた後、**会社名、所属業界の種類**を正しく入力し、**会社営業許可証**をアップロードし、**OK**をクリックして審査申請を送信し、手動での審査フローを待ちます。

![](https://qcloudimg.tencent-cloud.cn/raw/e3d3bb59025c79ac4d46f45c67d1cc27.png)
3. テスト版Licenseの作成に成功すると、発行されたLicense情報が画面に表示されます。この時点ではKeyとLicenseURLという2つのパラメータはまだ有効になっておらず、送信したものが審査によって承認されて初めて有効化され使用できるようになります。**SDKの初期化設定の際に、KeyとLicense URLの2つのパラメータを渡す必要があります。次の情報を適切に保存してください。**
![](https://qcloudimg.tencent-cloud.cn/raw/6b8d5e0cca6b37e136040a50a17d5099.png)

<dx-alert infotype="explain"> 
1. テスト版Licenseの有効期間内であれば、右側の**編集**をクリックして進み、Bundle IDとPackage Name情報を変更し、**OK**をクリックして保存することができます。ただし、それによって、このテストLicenseで有効なテスト版Tencent Effect機能モジュールが**新たに審査フローに入ってしまい**、承認されてからでなければ使用を継続できなくなる場合があります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2a4f9588cc7f0ba5131e631ace94d10.png" style="zoom: 67%;" />
2. Package NameまたはBundle Idがない場合は、「-」と入力します。
</dx-alert>

:::
::: 方法2：作成済みのテストアプリケーションで新機能モジュールのテストを申請する
作成済みのTencent Effectテストアプリケーションで新しい機能テストモジュールを申請したい場合は、次の手順で行います。
1. テストしたいアプリケーションを選択し、**新機能モジュールのテスト**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/31d21e8d61ed556276a44706a244d804.png)
2. 機能モジュールの**ハイグレードパッケージS1 - 04**/**アトミック機能X1-01**/**アトミック機能X1-02**にチェックを入れた後、**会社名、所属業界の種類**を正しく入力し、**会社営業許可証**をアップロードし、**OK**をクリックして審査申請を送信し、手動での審査フローを待ちます。 
<img src="https://qcloudimg.tencent-cloud.cn/raw/99f950a4bb1396e31d69f2c28cdab64f.png" style="zoom:50%;" />
:::
</dx-tabs>

3. 審査申請送信後のモジュールは**会社要件審査中**となります。審査にかかる時間は通常1～2業務日です。**審査情報を確認する**をクリックすると、送信した審査情報を確認することができます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a349ab1958dc407c362fad72485dab5d.png" style="zoom:67%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/34446b73133115d11e18b54393361b98.png" style="zoom:67%;" />
4. 審査で承認されると、Tencent Effect機能モジュールのステータスは**正常**となります。Tencent Effectテスト版Licenseの申請に成功し、Tencent Effect機能モジュールの利用を開始することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/516e3b714bd158a452022c4c563e0756.png)
>? **審査結果が不承認**の場合は、**審査結果**をクリックすると審査結果と審査の備考を確認することができ、備考の内容によって不承認の理由を知ることができます。**再審査を申し込む**をクリックし、審査情報を変更して送信してください。人の手による審査フローとなりますのでお待ちください。

![](https://qcloudimg.tencent-cloud.cn/raw/d787f5e69875a0de1294a8dd0ab519f3.png)

[](id:renewal_test)
### テスト版Licenseの更新
テスト版Licenseの初回申請の場合、デフォルトの有効期間は14日間となり、有効期間終了後に**1回**更新できます。機能モジュールの**Tencent Effect**の右側の**更新**をクリックし、**更新する**をクリックすると、この機能モジュールの有効期間を14日間延長することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/688ba0f794f4ec63857583a436d78e7a.png)

>? テスト版Licenseの有効期間は合計28日間で、**更新は一度しかできません**。引き続きご利用になりたい場合は、[正式版License](#create_formal)をご購入ください。

[](id:upgrade_test)
### テスト版Licenseのアップグレード
Tencent Effectモジュールのテスト版Licenseを正式版Licenseにアップグレードし、使用有効期間を延長したい場合は、先に[Tencent Effect正式版パッケージの選択と購入](https://buy.cloud.tencent.com/vcube?type=magic)を行い、その後次の操作を実行してください。
1.テスト版LicenseのTencent Effectモジュールの**アップグレード**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/d1915913278cbf6f3c188141cdcdea5f.png)
2. 機能モジュールアップグレード画面に進み、**今すぐバインド**をクリックし、バインドされていないTencent Effectパッケージを選択し、**OK**をクリックすると、同じパッケージ名の正式なアプリケーションをアップグレードして作成でき、同時にTencent Effectモジュールの正式版Licenseのロックが解除されます。発行審査は必要ありません。バインド可能なTencent Effectパッケージがない場合は、[リソースパック購入ページ](https://buy.cloud.tencent.com/vcube?type=magic)をクリックし、Tencent Cloud View Cubeリソースパック購入ページで購入できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9466fa0917c9220d849603ab6a29b190.png" style="zoom:50%;" />

[](id:formal)
## 正式版License
[](id:create_formal)
### 正式版Licenseの購入
具体的なシーンのニーズに応じて、[Tencent Effect SDK購入ページ](https://buy.intl.cloud.tencent.com/vcube)でSDKエフェクト機能を選択して購入し、それに応じた正式版Licenseの使用権限を取得することができます（有効期間は1年後の期限翌日の00:00:00（UTC+8）までです）。各バージョンのSDKの機能の違いについては、[課金概要](https://www.tencentcloud.com/document/product/1143/45376)をご参照ください。

具体的な手順は次のとおりです。
1. Tencent Effect正式版Licenseをバインドします。**正式なアプリケーションを新規作成してLicenseをバインドする**か、または**作成済みのアプリケーションでTencent Effect正式版モジュールのロックを解除し、Licenseをバインドする**という2種類の方法から選択して正式版Licenseのバインドを行うことができます。 
<dx-tabs>
::: 方法1：正式なアプリケーションを新規作成してLicenseをバインドする
1. [**Tencent Effectコンソール > モバイル端末License**](https://console.cloud.tencent.com/vcube)に進み、**正式版Licenseの新規作成**をクリックします。  
![](https://qcloudimg.tencent-cloud.cn/raw/1840aafe0ac1fc54485f9d4a4b15b98a.png) 
2. 正式アプリケーションの`App Name`、`Package Name`および`Bundle ID`情報を入力し、機能モジュールの**Tencent Effect**にチェックを入れ、**次のステップ**をクリックします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f128fdb87a0cc07762bbb75e86b460e9.png" style="zoom:50%;" />
3. リソース項目選択およびLicenseバインド画面に進み、**今すぐバインド**をクリックし、**バインドされていない**Tencent Effectパッケージ（バインド可能なリソースパックがない場合は、[リソースパック購入ページ](https://buy.cloud.tencent.com/vcube?type=magic)で購入できます）を選択し、**OK**をクリックすると、アプリケーションを作成して正式版Licenseを発行できます。 
<img src="https://qcloudimg.tencent-cloud.cn/raw/db5cf0bb61ea8063d25a11dfafb89e90.png" style="zoom:50%;" />

<dx-alert infotype="explain"> **OK**をクリックする前に、Bundle IDとPackage Nameが業務で使用しているパッケージ名の情報と一致しているかを再度確認する必要があります。ストアに送信したものと一致しない場合は、送信前に変更してください。 **正式版Licenseは一度送信に成功すると、License情報の変更ができなくなります**。 </dx-alert>

:::
::: 方法2：作成済みの公式アプリケーションでモジュールのロックを解除する
1. 追加したい**Tencent Effect**機能モジュールの正式アプリケーションを選択し、**新機能モジュールのロックを解除**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/7d00d56c1dd4c1658f4fde736276d322.png)
2. **Tencent Effect**を選択し、**次のステップ**をクリックします。  
<img src="https://qcloudimg.tencent-cloud.cn/raw/d88b7f921e294eafec2bbdbaab65edec.png" style="zoom:50%;" />
3. リソース項目選択およびLicenseバインド画面に進み、**今すぐバインド**をクリックし、**バインドされていない**Tencent Effectパッケージ（バインド可能なTencent Effectパッケージがない場合は、[リソースパック購入ページ](https://buy.intl.cloud.tencent.com/vcube)で購入できます）をクリックし、**OK**をクリックすると、アプリケーションに正式版Tencent Effect機能モジュールを生成することができます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/0df1ab29aec13532934eed6457b8936d.png" style="zoom:50%;" />)
:::
</dx-tabs>
2. Tencent Effect機能モジュールのステータスが**正常**となり、Tencent Effect正式版Licenseの申請に成功すると、Tencent Effect機能モジュールの利用を開始することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/75200f8c745038400c568ca5e4d241af.png)


[](id:upgrade_formal)
### 正式版Licenseの有効期間更新
[**Tencent Effect SDKコンソール > モバイル端末License管理**](https://console.tencentcloud.com/xmagic)にログインし、ページ上でTencent Effect正式版Licenseの有効期限を確認できます。 Tencent Effect正式版Licenseがすでに期限切れとなっている場合は、次の操作によって更新が可能です。
1. 有効期限を更新したいLicenseを選択し、Tencent Effectモジュール内の**更新**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/a4b37fc395ce6ea395541825167ad284.png)
2. 元のLicenseと**同タイプのパッケージ**のリソースを選択してバインドし、更新を行います。選択すると更新の開始時刻と終了時刻がリアルタイムに表示され、**OK**をクリックすると更新が完了します。バインド可能なTencent Effectパッケージがない場合は、[リソースパック購入ページ](https://buy.intl.cloud.tencent.com/vcube)をクリックして購入できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/decbe36048335926e3a964a6ae923fbe.png" style="zoom:50%;" />
>! 現時点では、パッケージの有効期限更新は同タイプのパッケージの更新のみサポートしています。バインドされているLicenseパッケージのタイプがS1 - 04の場合、更新時に選択できるのはS1 - 04のパッケージのみとなります。バインドするパッケージのタイプを変更したい場合は、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category)するか、または担当者までご連絡ください。

3. 更新後の有効期限の状況を確認します。
>! **Tencent Effect正式版Licenseは情報の変更をサポートしていません**。License情報を変更する必要がある場合は、リソースパックを購入後、Licenseの有効期限の更新は行わず、**アプリケーションを作成してLicenseをバインドする**をクリックして、再度アプリケーションを作成し、新規Licenseに新しいパッケージ名情報をバインドしてください。
