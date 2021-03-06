VODは [ホットリンク防止](https://intl.cloud.tencent.com/document/product/266/33984) 機能を提供して、実際のニーズに応じてビデオ再生URLで使用されるドメイン名に対して合理的にホットリンク防止を設定し、ユーザーのビデオ再生行為を制御します。

しかし、テストをしないで使用中のドメイン名にホットリンク防止を設定することには、以下のリスクがあります。

- 現行のネットワーク環境のユーザーの再生エラーを発生させることがある。
- 再生抑制の効果に至らない可能性がある。

例えば、開発者がビデオ再生URLの有効期間を制御する場合、[Keyホットリンク防止](https://intl.cloud.tencent.com/document/product/266/33986)を有効にする必要があります。

* 生成されたホットリンク防止の署名パラメータ`sign`の計算にエラーがある場合は、**ホットリンク防止を有効にすると、現行ネットワーク環境のすべてのビデオ再生にエラーが発生することがあります**。
* 生成されたホットリンク防止の期限切れ時間のパラメータ`t`が大きすぎると、**ホットリンク防止を有効にした後のビデオ再生URLがスケジュールどおりに期限切れになりません**。

このため、開発者はドメイン名に対してホットリンク防止を有効にする前に、予想に適合することを確認するために、まずテストを実行する必要があります。また、ホットリンク防止をテストすると同時に、現行ネットワーク環境のユーザーに影響を与えないようにする必要があります（ホットリンク防止が現行ネットワークに対して安全であることを保証するということ）。

## 安全なホットリンク防止テストの実現

VODは、安全なホットリンク防止テストソリューションを提供しています。

### 専門用語の説明
ソリューションを説明しやすくするために、以下の関連する専門用語をご紹介します。

* **デフォルトのVODドメイン名**：現行ネットワーク環境において、VODビデオの再生で使用される正式なドメイン名のことです。VODの「カスタムドメイン名」は「VODのデフォルトドメイン名」に設定できます（設定方法については[カスタムドメイン名](https://intl.cloud.tencent.com/document/product/266/35572)をご参照ください）。
* **VODテストドメイン名**：デバッグに使用されるテスト用ドメイン名。現行ネットワーク環境では使用してはいけません。デフォルトのドメイン名に設定することはお勧めしません。
* **正式なAppバックエンド**：ビジネスAppバックエンドサービス。現行ネットワーク環境のユーザーはここからビデオ再生URLを取得します。
* **テストAppバックエンド**：ビジネステスト環境のAppバックエンドサービス。 テストクライアントはここからビデオ再生URLを取得します。

### ソリューションの詳細

通常では、現行ネットワーク環境のユーザーは正式なビジネスAppバックエンドからビデオ再生URLを取得し、テストクライアントはビジネステストAppバックエンドからビデオ再生URLを取得し、2箇所から取得したURLのドメイン名は同じです（すべてVODデフォルトドメイン名）。ホットリンク防止テストのときは、VODデフォルトドメイン名を直接変更できません。変更すれば、現行ネットワーク環境のユーザーが影響を受けます。

<img src="https://main.qcloudimg.com/raw/85d3b79bc4255be32804c53438bc8ec2.png" width="450">

現行ネットワーク環境のユーザーに対するホットリンク防止テストの影響を回避するために、テストドメイン名を追加で準備しておく必要があります。現行ネットワーク環境で使用されるVODデフォルトドメイン名とは切り離します。ホットリンク防止をテストするときは、テストドメイン名のホットリンク防止設定のみを管理する必要があります。

VODは「テストドメイン名プロキシ」（IPは`122.152.250.73`）も提供します。テストクライアントのHOSTテーブルを変更して、VODデフォルトドメイン名をこのプロキシに解決する必要があります。 テストクライアントからのビデオ再生リクエストは、プロキシを経由してテストドメイン名に転送されます（下図の赤色のパス）。そして現行のネットワーク環境のユーザーからの再生リクエストは正式ドメイン名に転送されます（下図の黒色のパス）。

<img src="https://main.qcloudimg.com/raw/ea7c413d0bc993554b4b5521ffc7adcf.png" width="450">

このため、テストドメイン名のホットリンク防止を自由に変更し、テストAppバックエンドによって配布されたビデオ再生URLをテストできます。現行ネットワーク環境のユーザーへの影響を心配する必要はありません。

<img src="https://main.qcloudimg.com/raw/9d47fd2140a3bdc7a20aa6347407b009.png" width="450">

テストクライアントおよびテストAppバックエンドでホットリンク防止を十分に検証して誤りがないことを確認した後、順次以下の手順を実行できます。

1. 正式Appバックエンドによって配布されるビデオ再生URL規則を、テストAppバックエンドと一致するように修正します。
2. VODデフォルトドメイン名のホットリンク防止設定を、テストドメイン名と一致するように修正します。

このように、VODのデフォルトドメイン名のホットリンク防止を有効にして、テスト後に検証されたホットリンク防止設定を現行ネットワークに応用できます。

## 操作インスタンス

以下、Keyホットリンク防止を有効にして、ホットリンク防止テストの操作手順をご紹介します。

1. テストドメイン名のホットリンク防止を有効にします。
2. オリジナル再生URLを取得します。
3. テストクライアントは、オリジナルURLでビデオを再生できることをテストします。
4. テストクライアントのHOSTテーブルを変更します。
5. テストクライアントはオリジナルURLでビデオを再生できなくなります。
6. テストクライアントは、ホットリンク防止パラメータ付きのURLでビデオを再生できます。
7. 正式なAppバックエンドは、ホットリンク防止パラメータ付きURLを生成します。
8. VODデフォルトドメイン名はホットリンク防止を有効にします。

#### 背景

ユーザー（例の appid は`125xxx655`）はVODコンソールにログインして、 [【Domain Management】](https://console.cloud.tencent.com/vod/distribute-play/domain) で正式なドメイン名およびテストドメイン名を追加し、併せて正式ドメイン名をデフォルトドメイン名に設定します。初期状態のドメイン名は、デフォルトではKEYホットリンク防止は有効になっていません。

#### 1. テストドメイン名のホットリンク防止を有効にする

テストドメイン名を選択して【設定】をクリックし、【Keyホットリンク防止】に進みます。Keyホットリンク防止を起動して【Key生成】を使用して、1個のホットリンク防止Keyを作成します。【OK】をクリックして保存し、設定が有効になるのを待ちます。

#### 2. オリジナル再生URLを取得する

ビデオのオリジナル再生URLは、 [ホットリンク防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE.E5.8F.82.E6.95.B0) のないURLアドレスを示し、コンソールの [メディア資産管理](https://console.cloud.tencent.com/vod/media) から取得することができます。

#### 3. テストクライアントは、オリジナルURLでビデオを再生できることをテストする

![](https://main.qcloudimg.com/raw/a991036d94d654078c94a4b0c19d778d.png)
この時、テストクライアントはビデオのオリジナルURLで直接ビデオを再生できます。`curl`を実行すると返されるHTTPのステータスコードは200です。

#### 4. テストクライアントのHOSTテーブルを変更する

テスト端末のHOSTテーブル（Windows システムは`C:\Windows\System32\drivers\etc\hosts`、Macシステムは`/private/etc/hosts`）を変更して、レコード```122.152.250.73 テストドメイン名```を追加し、変更を保存します。

修正後は、```ping テストドメイン名```を実行して、HOSTの変更が有効か検査します。

#### 5. テストクライアントはオリジナルURLでビデオを再生できなくなる

HOSTテーブルを変更してから、テストクライアントはオリジナルURLでビデオを再生できなくなり、返されるHTTPステータスコードは403 Forbiddenになります。HOST テーブルが変更されたため、テストクライアントによって開始されたビデオ再生リクエストがプリセットVODテストドメイン名にマッピングされ、ビデオを再生する前に正しいホットリンク防止パラメータをURLに含める必要があるためです。

#### 6. テストクライアントは、ホットリンク防止パラメータ付きのURLでビデオを再生できる

 Keyホットリンク防止の [生成規則](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) に従って、ホットリンク防止パラメータ付きのURLを生成すれば、ビデオを再生できます。アドレスは`https://xxx.com/ca7xxx655/cfbxxx349/PkxxxIA.mov?t=5bd6be00&sign=18cxxx9deb`であり、```curl```を実行すると、 返されるHTTPステータスコードは200になります。

テストAppバックエンドはホットリンク防止規則に従って、ホットリンク防止パラメータ付きのURLを配布し、テストクライアントで検証を行います。

#### 7. 正式なAppバックエンドは、ホットリンク防止パラメータ付きURLを生成する

テスト環境が検証された後、正式なAppバックエンドはテストAppバックエンドと同じ規則に従って ホットリンク防止パラメータ付きのURLを配布します。

#### 8. VODデフォルトドメイン名はホットリンク防止を有効にする

先にコンソールで**テストドメイン名 **の【Keyホットリンク防止】を開いて、ホットリンク防止Keyをコピーします。**VODデフォルトドメイン名**の【Keyホットリンク防止】を開き、テストドメイン名のKeyを【ホットリンク防止Key】テキストボックスに貼り付けて、【OK】をクリックして保存します。

ドメイン名の設定が有効になったら、ホットリンク防止の設定は、現行ネットワーク環境で使用されるVODデフォルトドメイン名に適用され、正式に有効になります。
