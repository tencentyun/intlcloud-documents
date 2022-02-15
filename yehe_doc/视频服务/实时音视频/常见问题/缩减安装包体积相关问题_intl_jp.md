###  TRTC SDKのインテグレーション後、ファイル容量の増加はどのくらいですか？
TRTCの各バージョンのSDKで容量の増加は異なります。詳しくは、[SDK ダウンロード](https://intl.cloud.tencent.com/document/product/647/34615)をご参照ください。

### iOSのプラットフォームでインストールパッケージの容量を圧縮するにはどうすればいいですか？
<dx-tabs>
::: 方法一：ARM64アーキテクチャのみでパッケージ化（推奨）
 アップルiPhone5s以上のバージョンの携帯電話はいずれもx64 アーキテクチャのみでのパッケージ化をサポートできます。XCodeの中のBuild Settingで、Build Active Architecture Onlyの設定をYESにし、同時に、Valid Architecturesに arm64と書き込むだけで済みます。TRTC SDK のシングルアーキテクチャのipa増加量は僅か1.9Mです。
![](https://main.qcloudimg.com/raw/4aea00771567fcff58697bf5433ba0dd.png)
::: 
::: 方法二：BitCodeを起動
 アップルiPhone 5sとそれ以前のバージョンの携帯電話では、**プログラムの中の全てのサードパーティライブラリで BitCodeをサポートしている場合**、BitCodeを起動してインストールパッケージの容量を圧縮することができます。Build Settings > Build Optionsの中で Enable Bitcodeのオプションを開けば、BitCodeを起動できます。
 ![](https://main.qcloudimg.com/raw/516c0065d97eee4569a1d4061ba019cb.png)
2016年以降、アップルはそのXCode開発環境の中で、BitCodeコンパイルのオプションをサポートし始めました。BitCodeを立ち上げると、コンパイラが Appに対して 中間コードを生成し、実際のアセンブリのマシンコードとはなりません。ユーザーがApp Storeから ダウンロードしてインストールするのは、具体的な携帯電話のCPUアーキテクチャを対象に生成されたマシンコードです。そのためこの方法ではインストールパッケージの容量を大幅に圧縮できます。
:::
</dx-tabs>
### Androidのプラットフォームでインストールパッケージの容量を圧縮するにはどうすればいいですか？
<dx-tabs>
:::方法一：一部のsoファイルのみをパッケージ化
 Appを中国大陸のみで使用する場合は、`armeabi-v7a`アーキテクチャのsoファイルのみをパッケージ化すれば、インストールパッケージの容量増加を5M以内に圧縮できます。Appを Google Playストアに掲載したい場合は、`armeabi-v7a`と `arm64-v8a`の2つのアーキテクチャの soファイルをパッケージ化できます。
**具体的な操作方法**：現在のプログラムの build.gradleの中に `abiFilters "armeabi-v7a"`を追加してシングルアーキテクチャのso ファイルのパッケージ化を指定するか、または `abiFilters "armeabi-v7a","arm64-v8a"を追加してデュアルアーキテクチャの soファイルを指定します。
 - `armeabi-v7a` アーキテクチャの so ファイルのみでパッケージ化する（Google Playに掲載する必要がない）場合：
    ![](https://main.qcloudimg.com/raw/72065de8f9cd1c95b23fb797d383b527.png)
 - `armeabi-v7a` と `arm64-v8aの2つのアーキテクチャの so ファイルをパッケージ化する場合（Google Playに掲載）：
    ![](https://main.qcloudimg.com/raw/a6dcbef3c71fe9f2f7b5d52d6b0784ae.png)
:::
:::方法二：jarファイルのみでパッケージ化（インストール後にsoファイルをダウンロード）
 >! AppをGoogle Playに掲載したい場合は、この方法を使用しないでください。掲載できない可能性があります。
 
Android 版 SDKの容量は主にsoファイルから来るものです。インストールパッケージの容量増加を1M以内に圧縮したいのであれば、インストールしてからsoファイルをダウンロードする方式を検討することができます。
[](id:step1)
 
 1.  [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android) フォルダ下で、`LiteAVSDK_TRTC_x.x.xxx.zip` に似た名前がついた圧縮パッケージを見つけることができます。それを解凍して指定アーキテクチャのsoファイルを見つけます。
 2. [手順1](#step1)でダウンロードしたsoファイルをアップロードします。お客様のサーバー（またはTencent Cloudの [COS](https://intl.cloud.tencent.com/product/cos) Cloud Object Storageのサーバー）にアップロードし、ダウンロードURLを記録します(例：`http://xxx.com/so_files.zip`）。
 3. ユーザーがSDKの関連機能を立ち上げる前（例：ビデオ再生の開始前）に、先に loadingの動画を使って、「関連機能モジュールのローディング中」であることをユーザーに喚起します。
    ユーザーが待っている間に、Appは  `http://xxx.com/so_files.zip`に移動してsoファイルをダウンロードし、かつアプリケーションディレクトリの下に保存します（例：アプリケーションのルートディレクトリの下のfiles フォルダ）。このプロセスがキャリアの DNSハイジャックの影響を受けないように、ファイルダウンロード完了後に、soファイルの完全性を検証し、キャリアによるzip压缩パックの改ざんを防止してください。
 4. soファイルが全て揃うのを待ってから、`TXLiveBase`類（LiteAVSDKの最も早期の基本モジュール）の中の `setLibraryPath()`インターフェースを呼び出し、soダウンロードのターゲットパスをSDKに設定します。SDKはこれらのパスを辿って必要な soファイルをローディングし、関連機能を立ち上げます。
:::
</dx-tabs>

