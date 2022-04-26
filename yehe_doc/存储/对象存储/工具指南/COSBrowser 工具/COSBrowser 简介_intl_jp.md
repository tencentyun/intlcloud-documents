COSBrowserは、Tencent CloudがCOS用としてリリースしたビジュアルインターフェースツールで、より簡単な操作でCOSリソースのインタラクティブな表示・転送・管理を行うことができます。COSBrowserには現在、デスクトップとモバイル端末という2種類があります。詳細については、以下をご参照ください。

- [デスクトップの使用説明](https://intl.cloud.tencent.com/document/product/436/32565)
- [モバイル端末の使用説明](https://intl.cloud.tencent.com/document/product/436/32566)

## ダウンロードアドレス

<table>
   <tr>
      <th>COSBrowserカテゴリー</td>
      <th>サポートプラットフォーム</td>
      <th>システム要件</td>
      <th>ダウンロードアドレス</td>
   </tr>
   <tr>
      <td rowspan=3>デスクトップ</td>
      <td>Windows</td>
      <td>Windows 7 32/64ビット以上、Windows Server 2008 R2 64ビット以上</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe">Windows</a></td>
   </tr>
   <tr>
      <td>macOS</td>
      <td>macOS 10.13以上</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.dmg">macOS</a></td>
   </tr>
   <tr>
      <td>Linux</td>
      <td>グラフィカルインターフェースとサポートが必要です<a href="https://appimage.org">AppImage</a> 形式<br>
          注意：CentOSでクライアントを起動するには、<code>/cosbrowser.AppImage --no-sandbox</code>を実行する必要があります</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip">Linux</a></td>
   </tr>
   <tr>
      <td rowspan=2>モバイル端末</td>
      <td>Android</td>
      <td>Android 4.4以上</td>
      <td><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.apk">Android</a></td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>iOS 11以上</td>
      <td>iOS</td>
   </tr>
   <tr>
      <td>Web版</td>
      <td>Web</td>
      <td>Chrome/FireFox/Safari/IE10以上のブラウザ</td>
      <td><a href="https://cosbrowser.cloud.tencent.com/web">Web</a></td>
   </tr>
   <tr>
      <td>Uploaderプラグイン</td>
      <td>Web</td>
      <td>Chromeブラウザ</td>
      <td><a href="https://chrome.google.com/webstore/detail/cosbrowser-uploader/mggpkimgmmdbdbakdkaebhjhgomcmlnd">アプリストア</a>/<a href="https://cos5.cloud.tencent.com/cosbrowser/latest-chrome.zip">オフラインダウンロード</a></td>
   </tr>
</table>

## デスクトップ機能リスト

COSBrowserデスクトップはリソース管理に重点を置いており、ユーザーはCOSBrowserからデータを一括でアップロード・ダウンロードすることができます。

> !COSBrowserデスクトップは、システムによって設定されたプロキシを使用してインターネットへの接続を試みます。プロキシ設定が正常であることを確認するか、インターネットに接続できないプロキシ設定を無効にしてください。
>
> - Windowsユーザーは、OSの「インターネットオプション」で確認することができます。
> - macOSユーザーは、「ネットワーク環境設定」で確認することができます。
> - Linuxユーザーは、システム設定 > ネットワーク > ネットワークプロキシで確認することができます。

COSBrowserデスクトップは、以下の機能をサポートします。

| 機能                                                         | 機能説明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [バケットの作成/削除](https://intl.cloud.tencent.com/document/product/436/32565#createordelete) | バケットの作成と削除をサポートします                                         |
| [バケットの詳細情報の表示](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | バケットの基本情報の表示をサポートします                                       |
| [統計データの表示](https://intl.cloud.tencent.com/document/product/436/32565#count)           | バケットの現在のストレージ容量とオブジェクト総数の表示をサポートします                         |
| [権限管理](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | バケットやオブジェクトに関する権限の変更をサポートします                               |
| [バージョン管理の設定](https://intl.cloud.tencent.com/document/product/436/32565#viewbucket) | バケットのバージョン管理の有効化と一時停止をサポートします                                 |
| [アクセスパスの追加](https://intl.cloud.tencent.com/document/product/436/32565#addaccess) | アクセスパスの追加をサポートします                                             |
| [ファイル/フォルダのアップロード](https://intl.cloud.tencent.com/document/product/436/32565#upload) | ファイルまたはフォルダのバケットへの個別アップロード、一括アップロード、差分アップロードをサポートします         |
| [ファイル/フォルダのダウンロード](https://intl.cloud.tencent.com/document/product/436/32565#upload) | ファイルまたはフォルダのローカルへの個別ダウンロード、一括ダウンロード、差分ダウンロードをサポートします         |
| [ファイル/フォルダの削除](https://intl.cloud.tencent.com/document/product/436/32565#delete) | バケット内のファイルやフォルダの個別削除、一括削除をサポートします                 |
| [ファイルの同期](https://intl.cloud.tencent.com/document/product/436/32565#synchronization) | ローカルファイルのバケットへのリアルタイム同期をサポートします                             |
| [ファイルのコピーと貼り付け](https://intl.cloud.tencent.com/document/product/436/32565#copy) | 1つのディレクトリから別のディレクトリへのファイルまたはフォルダへの個別コピー、一括コピーをサポートします    |
| [ファイルのリネーム](https://intl.cloud.tencent.com/document/product/436/32565#rename) | バケット内のファイルのリネームをサポートします                                     |
| [フォルダの新規作成](https://intl.cloud.tencent.com/document/product/436/32565#newfolder) | バケット内でのフォルダの新規作成をサポートします                                     |
| [ファイルの詳細を表示](https://intl.cloud.tencent.com/document/product/436/32565#view) | バケット内のファイルの基本情報の表示をサポートします                              |
| [ファイルリンクの発行](https://intl.cloud.tencent.com/document/product/436/32565#generatelinks) | 一時的な署名をリクエストすることで、制限時間のあるファイルへのアクセスリンクの発行をサポートします         |
| [ファイル/フォルダの共有](https://intl.cloud.tencent.com/document/product/436/32565#share) | ファイルとフォルダの共有と、共有の有効時間の設定をサポートします         |
| [ファイルURLのエクスポート](https://intl.cloud.tencent.com/document/product/436/32565#export) | ファイルURLの一括エクスポートをサポートします         |
| [ファイルプレビュー](https://intl.cloud.tencent.com/document/product/436/32565#preview) | バケット内のメディアファイル（画像・ビデオ・オーディオ）のプレビューをサポートします               |
| [ファイル検索](https://intl.cloud.tencent.com/document/product/436/32565#searchfile) | プレフィックス検索によるバケット内のファイル検索をサポートします                 |
| [バケットの検索](https://intl.cloud.tencent.com/document/product/436/32565#searchbuckete) | 作成済みのバケットの検索をサポートします                                       |
| [バージョンの履歴またはファイルフラグメントの表示](https://intl.cloud.tencent.com/document/product/436/32565#viewfiles) | <li>バージョン管理が有効になっているバケット内のファイルのバージョン履歴の表示をサポートします<br><li>バケット内のファイルフラグメントの詳細の表示をサポートします           |
| [ネットワークプロキシの設定](https://intl.cloud.tencent.com/document/product/436/32565#sets) | COSにアクセスするためのネットワークプロキシの設定をサポートします                                   |
| [同時実行数の設定](https://intl.cloud.tencent.com/document/product/436/32565#sets) | ファイルのアップロード・ダウンロードの同時実行数の設定をサポートします                          |
| [転送チャンク数の設定](https://intl.cloud.tencent.com/document/product/436/32565#sets) | ファイルのマルチパートアップロード、ダウンロードのチャンク数の設定をサポートします                           |
| [転送失敗時の再試行回数の設定](https://intl.cloud.tencent.com/document/product/436/32565#sets) | ファイルのアップロードとダウンロードが失敗した場合の再試行回数の設定をサポートします                       |
| [アップロードの二次チェックの設定](https://intl.cloud.tencent.com/document/product/436/32565#sets) | バケットにアップロードされたファイルの二次チェックをサポートします                       |
| [シングルスレッド速度制限の設定](https://intl.cloud.tencent.com/document/product/436/32565#sets) | シングルスレッドのアップロードとダウンロードの速度制限の設定をサポートします |
| [ローカルログの表示](https://intl.cloud.tencent.com/document/product/436/32565#sets) | COSBrowserへのユーザー操作記録のローカルログ形式による保存をサポートします       |

## モバイル端末機能リスト

COSBrowserモバイル端末は、リソースの表示とモニタリングに重点を置いており、ユーザーはCOSのストレージ量やトラフィックなどのデータをいつでもどこでもモニタリングすることができます。COSBrowserモバイル端末でサポートされている機能については、[モバイル端末機能リスト](https://intl.cloud.tencent.com/document/product/436/41616)をご参照ください。

## ログの更新

- デスクトップ更新ログ：[changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md)。
- モバイル端末更新ログ：[changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md)。

## フィードバックと提案

COSBrowserの使用に関してご質問やご提案がございましたら、フィードバックをお寄せください。

- デスクトップのフィードバック：[issues](https://github.com/tencentyun/cosbrowser/issues)。
- モバイル端末のフィードバック：[issues_mobile](https://support.qq.com/embed/phone/67467)。
