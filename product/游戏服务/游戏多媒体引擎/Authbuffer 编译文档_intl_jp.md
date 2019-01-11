## 概要
Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここではGME Authbufferのコンパイル技術文書を紹介します。

## コンパイルの詳細な手順

### 1.関連するファイルをダウンロード
[こちらをクリック](https://main.qcloudimg.com/raw/1fdb3269055bacb09695cd6014af1d0b.zip)してGME Authbufferに関連するファイルをダウンロードします。


### 2.関連するファイルをLinuxに転送
ダウンロードされたzip形式のファイルをLinuxに転送します。


### 3.関連するファイルを解凍
ダウンロードされたzip形式のファイルを解凍します。


### 4.プロジェクトディレクトリにアクセス
関連するコードについては、`cd authbuffer/build/linux/`を参照してください



### 5.makeを実行
makeを実行して、動的ライブラリを生成します。
パス：`[個人フォルダ]/authbuffer/build/linux`
![image](https://main.qcloudimg.com/raw/a97ab83b76f2ea68ce7315828224e99b.png)


### 6.実行可能なファイル
実行可能なファイルのパス：`[個人フォルダ]/authbuffer/bin/linux/libAuthbuffer.so`
![image](https://main.qcloudimg.com/raw/2f1d265631137955d1ab890790ab8d14.png)

