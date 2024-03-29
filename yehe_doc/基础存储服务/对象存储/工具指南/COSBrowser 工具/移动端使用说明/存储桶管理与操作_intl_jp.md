>?
>この機能説明はモバイル端末用iOS 2.7.6バージョンの例です。その他のバージョンでは違いがありますので、[更新ログ](https://github.com/TencentCloud/cosbrowser/blob/master/changelog_mobile.md)をご参照ください。
>



<span id="ViewTheBucketList"></span>
## バケットリストの表示

COSBrowserモバイル端末ではバケットリストをリージョン単位で表示し、リージョンのカテゴリーによってバケットを確認することができます。画面内のリソースアイコンをクリックすると、作成済みのバケットを確認できます。


<span id="AddAccessPath"></span>
## アクセスパスの追加

バケットリストへのアクセス権限を持たないサブアカウントでログインしている場合、バケットリストページ右上隅の**アクセスパスの追加**をクリックすると、指定のパスを追加してバケットまたはディレクトリ管理リソースに入ることができるようになります。

>? この機能はサブアカウントでのみサポートしています。


#### 操作手順

1. バケットリストページに進み、右上隅の**+**をクリックします。
2. ポップアップした操作リストで、**アクセスパスの追加**をクリックし、ルートアカウントによる権限承認を受けているアクセスパスを入力すれば完了です。


<span id="CreateBucket"></span>
## バケットの作成

COSBrowserモバイル端末によってバケットを作成することができます。バケットを作成する際は名前、リージョン、アクセス権限を指定する必要があります。

#### 操作手順

1. バケットリストページで、右上隅の**+**をクリックします。
2. ポップアップした操作リストで、**バケットの作成**をクリックします。
3. ポップアップしたバケット作成ページで、次の情報を設定します。
 - **名前**：カスタマイズするバケット名を入力してください。設定後に変更することはできません。命名については、バケットの[命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。
 - **所属リージョン**：お客様のビジネス（またはユーザー数）が比較的集中している物理的なエリアに対応するCOSリージョンを選択してください。設定後に変更することはできません。リージョンの詳細情報については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。
 - **アクセス権限**：バケットにはデフォルトで、プライベート読み取り/書き込み、パブリック読み取り/プライベート書き込み、およびパブリック読み取り/書き込みという3種類のアクセス権限が提供されています。設定後に変更することはできません。詳細については、[バケットのアクセス権限](https://intl.cloud.tencent.com/document/product/436/13315)をご参照ください。
4. 情報に誤りがないことを確認後、**OK**をクリックするとバケットを作成できます。
バケットリスト画面で、先ほど作成したバケットを確認できます。


<span id="SearchBucket"></span>
## バケットの検索

バケット数が多い場合は、バケットリストページの上にある検索バーにバケット名を入力して照会できます。現在はバケット名のあいまい一致検索をサポートしています。


<span id="ViewBucketBasicInfor"></span>
## バケット基本情報の確認

1. バケットリストページで操作したいバケットを見つけ、右側の**...**をクリックします。
2. ポップアップした操作リストで**詳細**をクリックすると、バケットの基本情報を確認できます。
基本情報には、バケット名、リージョン、作成時間およびマルチAZ有効化の有無が含まれます。


<span id="BucketPrivilegeManagement"></span>
## バケット権限管理

COSモバイル端末によって、バケットへのアクセス権限の設定または変更を行うことができます。COSは、以下2種類の権限タイプの設定をサポートしています。
- **パブリック権限**：プライベート読み取り/書き込み、パブリック読み取りプライベート書き込み、およびパブリック読み取り/書き込みです。パブリック権限の説明については、バケット概要の[権限のタイプ](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。
- **ユーザー権限**：ルートアカウントは、デフォルトではバケットのすべての権限を所有しています（完全制御）。またCOSは、サブアカウントに対するデータ読み取り、データ書き込み、権限読み取り、権限書き込み、さらには**完全制御**の最高権限の付与もサポートしています。


1. バケットリストページに進み、アクセス権限を設定または変更したいバケットを見つけ、右側の**...**をクリックします。
2. ポップアップした操作リストで**権限**をクリックすると、バケット権限ページに進むことができます。


<span id="ModifyPublicPermissions"></span>
### パブリック権限の変更

バケット権限ページでパブリック権限設定項目をクリックすると、パブリック権限を変更することができます。

<span id="SetUserPermissions"></span>
### ユーザー権限の設定

バケット権限ページでユーザーの追加をクリックすると、バケットのアクセス権限を設定することができます。


<span id="EditDeleteUserPermissions"></span>
### ユーザー権限の編集または削除

削除または編集したいユーザー権限を選択して左にスワイプすると、編集・削除ボタンがポップアップします。対応するボタンをクリックすると、その行のユーザー権限を編集または削除することができます。


<span id="OpenGlobalAcceleration"></span>
## グローバルアクセラレーションの有効化

COSBrowserでバケットのグローバルアクセラレーション機能を有効化することによって、世界各地のユーザーがバケットにスピーディーにアクセスしやすくなり、ビジネスへのアクセス成功率と業務の安定性を向上させることができます。グローバルアクセラレーション機能によって、アップロードとダウンロードを高速化することができます。
>? グローバルアクセラレーション機能を有効化しても、元のバケットのデフォルトドメイン名に影響を与えることなく、通常どおり使用することができます。
>


#### 操作手順

1. バケットリストページに進み、グローバルアクセラレーション機能を設定したいバケットを見つけ、バケット右側の**...**をクリックします。
2. ポップアップした操作バーで**転送**をクリックし、転送リストページに進みます。
3. グローバルアクセラレーション設定項目をクリックし、実際のニーズに応じてグローバルアクセラレーションの有効または無効状態を変更します。


<span id="BucketTransportConfig"></span>
## バケット転送設定

あるバケットをカスタムドメイン名によって転送したい場合は、このページで設定を行うことができます。

<span id="SetUploadDomainName"></span>
### アップロードドメイン名の設定

バケットでグローバルアクセラレーション機能を有効化している場合、そのバケットにファイルをアップロードする際に使用するグローバルアクセラレーションドメイン名を指定できます。アップロードドメイン名の設定完了後、バケットはそのドメイン名を優先的に使用してアップロードを行います。

<span id="SetDownloadDomainName"></span>
### ダウンロードドメイン名の設定

バケットにカスタムオリジンサーバードメイン名を設定している場合、そのバケットでファイルをダウンロードする際にカスタムオリジンサーバードメイン名を使用するよう指定できます。ダウンロードドメイン名の設定完了後、バケットはそのドメイン名を優先的に使用してダウンロードを行います。

