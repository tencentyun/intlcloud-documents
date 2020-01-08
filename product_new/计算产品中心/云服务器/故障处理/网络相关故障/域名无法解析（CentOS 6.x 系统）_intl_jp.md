## 事象の説明
CentOS 6.x OSのCVMを再起動するか、`service network restart` コマンドを実行した後、CVMはドメイン名を解析できない場合があります。また、`/etc/resolv.conf` 設定ファイルを表示すると、DNS情報がクリアされていることがわかりました。

## 考えられる原因
CentOS 6.x OSでは、grep のバージョンが異なるため、initscriptsのバージョンが 9.03.49-1より低い場合、バグがあります。

## 解決方法
initscriptsを最新バージョンにアップグレードし、DNS情報を再生成します。

## 処理手順
1. CVM にログインします。
2. 次のコマンドを実行して、initscripts のバージョンを確認し、9.03.49-1より低いバージョン（バグが潜在する）であるかを確認します。
```
rpm -q initscripts
```
次のような情報が返されます：
```
initscripts-9.03.40-2.e16.centos.x86_64
```
initscriptsのバージョンがinitscripts-9.03.40-2 であり、既存の問題バージョン（initscripts-9.03.49-1）より低く、DNS 情報がクリアになるリスクがあることが分かります。
3. 次のコマンドを実行して、initscripts を最新バージョンにアップグレードし、DNS 情報を再生成します。
```
yum makecache
yum -y update initscripts
service network restart
```
3. アップグレードが完了したら、次のコマンドを実行して、initscripts のバージョン情報を確認し、アップグレードが成功したかどうかを確認します。
```
rpm -q initscripts
```
次のような情報が返されます：
```
initscripts-9.03.58-1.el6.centos.2.x86_64
```
表示されたバージョンは以前のバージョンと異なり、initscripts-9.03.49-1バージョンより高く、アップグレードが成功していることが分かります。
