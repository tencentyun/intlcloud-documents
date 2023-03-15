**Tencent Effect SDKは美顔エフェクトに関連する機能をご提供します。無料のテスト版Licenseを申請するだけでアクセス体験が可能です。最長で28日間お試しいただけます。**

[](id:test)
## モバイル端末テスト版License

### テスト版Licenseの申請[](id:create_test)

Tencent Effectモジュールのテスト版License（無料テスト版の有効期間は14日間です。1回に限り継続可能で、計28日間となります）を無料で申請し、体験することができます。
テスト版Licenseはご自身のニーズに応じた機能を選んで申請できます。美顔エフェクトについてはパッケージとアトミック機能のテスト申請が可能です。このうちパッケージでは最上級バージョンのS1 - 04の権限発行のみサポートしており、このバージョンではTencent Effect SDKパッケージのすべての機能を試すことができます。最上級バージョンS1 - 04の機能については、[機能説明](https://intl.cloud.tencent.com/document/product/1143/45376)をご参照ください。パッケージS1-04にはX1-01人物画像分割機能が含まれており、その他の機能は含まれません。

>! **Tencent Effectの機能モジュールは申請後、審査を経てからでなければ権限が発行されません**。テスト版の有効期限は審査によって承認された時刻を基準に算出します。試用期間終了後にテスト継続の申請を行う場合、継続期間の有効期限はテスト継続の申請を行った時刻を基準に算出します。
>- Tencent Effect機能モジュールテスト版の審査情報を送信すると**ステータスが審査中**となります。審査にかかる時間は通常1～2業務日です。審査情報送信日時が`2022-05-24 12:47:33（UTC+8）`、審査承認日時が`2022-05-24 15:23:46（UTC+8）`の場合、開始日時は`2022-05-24 15:23:46（UTC+8）`、14日後の有効期限は`2022-06-09 00:00:00（UTC+8）`となります。
>- 無料で1回継続する際、14日間の試用期間内に継続を申請した場合、有効期限は`2022-06-23 00:00:00（UTC+8）`となります。14日間の試用期間終了後に継続を申請した場合、継続の申請時刻が`2022-08-06 22:26:20（UTC+8）`であれば、継続の有効期限は`2022-08-22 00:00:00（UTC+8）`となります。

モジュールのテストを申請します。**テスト版Licenseを新規作成して機能モジュールのテストを申請する**か、または**作成済みのテストアプリケーションで新機能モジュールのテストを申請する**という2種類の方法から選択して、テスト版Licenseを作成することができます。
<dx-tabs>
::: 方法1：テスト版Licenseを新規作成して機能モジュールのテストを申請する

1. [**Tencent Effect SDKコンソール > モバイル端末License**](https://console.tencentcloud.com/xmagic)にログインし、**テスト版Licenseの新規作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/84f8ab5111e32c16ef6553b14ac72fd7.png)
2. 実際の必要性に応じて`App Name`、`Package Name`、`Bundle ID`を入力し、テストしたい機能である**ハイグレードパッケージS1 - 04**、**アトミック機能X1-01**、**アトミック機能X1-02**を選択し、チェックを入れた後、**会社名、所属業界の種類**を正しく入力し、**会社営業許可証**をアップロードし、**OK**をクリックして審査申請を送信し、手動での審査フローを待ちます。
 
![](https://qcloudimg.tencent-cloud.cn/raw/0d4f80aa8fd068a9d562ee5246a1e63a.png)
3. テスト版Licenseの作成に成功すると、発行されたLicense情報が画面に表示されます。この時点ではKeyとLicenseURLという2つのパラメータはまだ有効になっておらず、送信したものが審査によって承認されて初めて有効化され使用できるようになります。**SDKの初期化設定の際に、KeyとLicense URLの2つのパラメータを渡す必要があります。次の情報を適切に保存してください。**
![](https://qcloudimg.tencent-cloud.cn/raw/d2bec2a1877a5b1ac83a4ae07e30db39.png)

<dx-alert infotype="explain"> 
1. テスト版Licenseの有効期間内であれば、右側の**編集**をクリックして進み、Bundle IDとPackage Name情報を変更し、**OK**をクリックして保存することができます。ただし、それによって、このテストLicenseで有効なテスト版Tencent Effect機能モジュールが**新たに審査フローに入ってしまい**、承認されてからでなければ使用を継続できなくなる場合があります。
![](https://qcloudimg.tencent-cloud.cn/raw/733ce3011060a2c552435ebe7115d643.png)
2. Package NameまたはBundle Idがない場合は、「-」と入力します。</dx-alert>

:::
::: 方法2：作成済みのテストアプリケーションで新機能モジュールのテストを申請する
作成済みのTencent Effectテストアプリケーションで新しい機能テストモジュールを申請したい場合は、次の手順で行います。
1. テストしたいアプリケーションを選択し、**新機能モジュールのテスト**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/5ec68592f2bb1f24335b15d6bff1a384.png)
2. 機能モジュールの**ハイグレードパッケージS1 - 04**/**アトミック機能X1-01**/**アトミック機能X1-02**にチェックを入れた後、**会社名、所属業界の種類**を正しく入力し、**会社営業許可証**をアップロードし、**OK**をクリックして審査申請を送信し、手動での審査フローを待ちます。 
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ee87ffbd3015d1ed31176bc48133595.png" style="zoom:80%;" />
:::
</dx-tabs>

3. 審査申請送信後のモジュールは**会社要件審査中**となります。審査にかかる時間は通常1～2業務日です。**審査情報を確認する**をクリックすると、送信した審査情報を確認することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/a27c350d9de411a9b629318703cbe2a4.png)
![](https://qcloudimg.tencent-cloud.cn/raw/4924c69299fa4d78ba7905a9111433af.png)
4. 審査で承認されると、Tencent Effect機能モジュールのステータスは**正常**となります。Tencent Effectテスト版Licenseの申請に成功し、Tencent Effect機能モジュールの利用を開始することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/f7e039ac73e24766cbaa240b98b06a4c.png)
>? **審査結果が不承認**の場合は、**審査結果**をクリックすると審査結果と審査の備考を確認することができ、備考の内容によって不承認の理由を知ることができます。**再審査を申し込む**をクリックし、審査情報を変更して送信してください。人の手による審査フローとなりますのでお待ちください。
![](https://qcloudimg.tencent-cloud.cn/raw/7e2e93d6e4091fbcab1bf9c865868bd5.png)

[](id:renewal_test)
### テスト版Licenseの更新
テスト版Licenseの初回申請の場合、デフォルトの有効期間は14日間となり、有効期間終了後に**1回**更新できます。機能モジュールの**Tencent Effect**の右側の**更新**をクリックし、**更新する**をクリックすると、この機能モジュールの有効期間を14日間延長することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/95f05996f1ae77f5b32fb051d3490c68.png)

>? テスト版Licenseの有効期間は合計28日間で、**更新は一度しかできません**。引き続きご利用になりたい場合は、[正式版License](#create_formal)をご購入ください。

[](id:upgrade_test)
### テスト版Licenseのアップグレード
Tencent Effectモジュールのテスト版Licenseを正式版Licenseにアップグレードし、使用有効期間を延長したい場合は、先に[Tencent Effect正式版パッケージの選択と購入](https://buy.cloud.tencent.com/vcube?type=magic)を行い、その後次の操作を実行してください。
1.テスト版LicenseのTencent Effectモジュールの**アップグレード**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/7d0508a70907b37be34ee78bae12c118.png)
2. 機能モジュールアップグレード画面に進み、**今すぐバインド**をクリックし、バインドされていないTencent Effectパッケージを選択し、**OK**をクリックすると、同じパッケージ名の正式なアプリケーションをアップグレードして作成でき、同時にTencent Effectモジュールの正式版Licenseのロックが解除されます。発行審査は必要ありません。バインド可能なTencent Effectパッケージがない場合は、[リソースパック購入ページ](https://buy.cloud.tencent.com/vcube?type=magic)をクリックし、Tencent Cloud View Cubeリソースパック購入ページで購入できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/20688364d5736456e24b29840c67140f.png" style="zoom:67%;" />
