## 操作シナオリ

Linux インスタンスには、NTPサービスを同期させるためNTPDateとNTPDの2つの方法が用意されています。NTPDateは強制的に即時更新するために使用でき、NTPDは体系的な方法として使用できます。 NTPDateサービスは、新しいインスタンスに使用できますが、ntpd はビジネスを実行しているインスタンスに対して使用することを推奨します。このドキュメントでは、CentOS 7.5 OSを使用して、CVMでNTPDateからNTPDに変換する方法について説明します。  

## 前提条件
NTPサービスの通信ポートは、UDP 123です。NTPサービスに変換する前に、UDP ポート123 をインターネットに開放することを確認してください。
このポートが開放されていない場合、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。

## 操作手順

### NTPDateをNTPDに手動で変換する
#### NTPDateのシャットダウン
1. 次のコマンドを実行して、crontab設定をエクスポートし、NTPDateをフィルタリングします。
```
crontab -l |grep -v ntpupdate > /tmp/cronfile
```
2. 次のコマンドを実行して、NTPDate設定を更新します。
```
crontab /tmp/cronfile
```
3. 次のコマンドを実行して、`rc.localファイルを変更します。
```
vim rc.local
```
4. 「**i**」を押して編集モードに切り替え、ntpupdateの設定行を削除します。
5. 「**Esc**」キーを押して、「**:wq**」を入力し、ファイルを保存してから戻ります。

#### NTPDの設定
1. 次のコマンドを実行して、NTPサービスの設定ファイルを開きます。
```
vi /etc/ntp.conf
```
2. **i**キーを押して編集モードに切り替え、サーバーの関連設定を見つけ、サーバーを、設定するターゲットNTPクロックソースサーバ（`time1.tencentyun.com`など）に変更し、一時的に不要なNTPクロックソースサーバを削除します。以下の通りです。
![serverの設定](https://main.qcloudimg.com/raw/643dc5bbd2a42307ec10b5d38f756dda.png)
3. 「**Esc**」キーを押し、「**:wq**」を入力し、ファイルを保存してから戻ります。


### NTPDateをNTPDへ自動変換
1. `ntpd_enable.sh`スクリプトをダウンロードします。
```
wget https://image-10023284.cos.ap-shanghai.myqcloud.com/ntpd_enable.sh
```
2. 次のコマンドを実行し、`ntpd_enable.sh`スクリプトを使用してNTPDateをNTPDに変換します。
```
sh ntpd_enable.sh
```



