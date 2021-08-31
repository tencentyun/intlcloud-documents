## 設定シナリオ

back-to-originリクエストのURLをオリジンサーバーと一致するURLに変更する必要がある場合、Tencent Cloud CDNはback-to-origin URL書き換え設定機能を提供しています。

>! ECDNドメイン名は、現時点では、この機能の設定をサポートしていません。


## 設定ガイド

### 設定の確認

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニューバーで【Domain Management】を選択し、ドメイン名操作列の【管理】をクリックして、ドメイン名設定画面に入ります。Tabを【back-to-origin設定】に切り替えると、【Origin URL書き換え設定】が表示されます。
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### ルールの追加

必要に応じて書き換えルールを追加できます。【ルールの追加】をクリックします。
<img src="https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg" style="height:300px"/>


**設定の制約**

- 1つのドメイン名につき、最大100件の書き換えルールを追加できます。
- 複数あるルールは優先順位を変更できます。下部の優先順位が上部のものよりも高くなります
- 書き換え予定のback-to-origin URL： `/` で始まり、デフォルトはプレフィックス一致で、フルパス一致（例：/test/a.jpg）とワイルドカード `*` 一致（例：/test/\*/\*.jpg）もサポートします。ファイルディレクトリを指定する場合は、「/」で終わることはできません（例：/test）。
- 目標back-to-origin Host：デフォルトは現在のドメイン名です。修正は可能で、`http://`または`https://` ヘッダーを含みません。
- 目標back-to-originパス： `/` で始まり（例：/newtest/b.jpg）、ワイルドカード `*` は `$n` でキャプチャできます（n=1,2,3...、例：/newtest/$1/$2.jpg）。ファイルディレクトリを指定する場合は、「/」で終えることはできません（例：/test）。
- ワイルドカード `*` は最大5件入力できます。キャプチャのプレースホルダー `$n` は最大10件入力できます。
- 中国語のコンテンツはサポートしていません。目標back-to-origin Hostは250文字以内とし、その他の入力欄のコンテンツは1024文字以内とします。



## 設定例：

アクセラレーションドメイン名`www.test.com`の** back-to-origin URL書き換え設定**を行う場合は次のとおりとなります。
![](https://main.qcloudimg.com/raw/eb34fde06561eb2c2cfe7afc9afc4d77.png)

上記設定の場合、実際のback-to-originの状況は次のとおりです。
- back-to-originリクエスト`www.test.com/images/1.jpg`は第1、2、3条のルールにヒットした場合、下部の優先順位が最も高く、実際のback-to-originリクエストは`www.test.com/index.html`になります。
- back-to-originリクエスト`www.test.com/images`は第2条のルールにヒットした場合、実際のback-to-originリクエストは`www.test.com/goodboy.html`になります。
