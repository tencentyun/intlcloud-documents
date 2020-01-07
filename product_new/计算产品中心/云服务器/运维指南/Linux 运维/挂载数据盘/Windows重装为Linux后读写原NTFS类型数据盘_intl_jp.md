通常、WindowsファイルシステムはNTFSまたはFAT32形式であり、Linuxファイルシステムの形式はEXTシリーズです。OSがWindowsからLinuxへリインストールした後、OSの種類が変更され、データディスクは元の形式のままです。リインストールしたOSはデータディスクのファイルシステムにアクセスできない可能性があります。リインストールしたLinux CVMで以下の操作を実行することにより元のWidowsシステムのデータディスクのデータを読み取ることができます。

1) Linuxシステムで以下のコマンドを使用してntfsprogsをインストールすると、LinuxがNTFSファイルシステムを利用できるようにします。

```
yum install ntfsprogs
```

2) WindowsのデータディスクをLinux CVMにマウントします。データディスクが既にマウントされている場合は、この手順をスキップしてください。

Tencent Cloudのコンソールにログインして、【CVM】-【Cloud Block Storage】タブに入り、マウント対象のWindowsデータディスク【詳細】-【クラウドホストにマウントする】ボタンをクリックします。ポップアップボックスでリインストール後のLinux CVMを選択して、【OK】ボタンをクリックします。

3) コマンド`parted -l`を使用して、Windowsからマウントされたデータディスクを確認します。
![](http://mccdn.qcloud.com/static/img/f0839d9209bc0927bd5293b45fdc7608/image.png)

4）コマンド `mount -t ntfs-3gデータディスクパスマウントポイント` を使用してデータディスクをマウントします。
![](http://mccdn.qcloud.com/static/img/cab81165b08034f2c300a2f30fccc8a4/image.png)

5）このファイルシステムを認識できるため、マウントされたデータディスクをLinuxシステムによって直接読み書きできます。