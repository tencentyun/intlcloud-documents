##故障について
コマンドの実行またはシステム起動のプロセスで、コマンドが見つからないか、またはlibファイルが見つからないなどのエラー情報が発生します。


## 考えられる原因
以下に示すとおり、CentOS 7、CentOS 8、Ubuntu 20などのシステムのbin、sbin、lib、lib64はソフトリンクです。
```
lrwxrwxrwx   1 root root     7 Jun 19  2018 bin -> usr/bin
lrwxrwxrwx   1 root root     7 Jun 19  2018 lib -> usr/lib
lrwxrwxrwx   1 root root     9 Jun 19  2018 lib64 -> usr/lib64
lrwxrwxrwx   1 root root     8 Jun 19  2018 sbin -> usr/sbin
```
ソフトリンクが削除された場合は、コマンドの実行またはシステム起動のプロセスでエラーが発生します。


## ソリューション
[処理手順](#ProcessingSteps)を参照して、必要なソフトリンクを調べて作成してください。


## 処理手順[](id:ProcessingSteps)
1. レスキューモードに進みます。
2. その中の`mount`、`chroot` などのコマンドを実行します。そのうち、`chroot`コマンドを実行した場合：
 - エラーがある場合は、`cd /mnt/vm1`を実行します。
 - エラーがない場合は、`cd /`を実行します。
3. 以下のコマンドを実行して、対応するソフトリンクがあるかどうかを確認します。
```
ls -al / | grep -E "lib|bin"
```
 - ソフトリンクがある場合は、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category)して連絡し、サポートを受けてください。
 - ソフトリンクがない場合は、必要に応じて以下のコマンドを実行して、対応するソフトリンクを作成してください。
```
ln -s usr/lib64 lib64
ln -s usr/sbin sbin
ln -s usr/bin bin
ln -s usr/lib lib
```
4. 以下のコマンドを実行して、ソフトリンクをチェックします。
```
chroot /mnt/vm1 /bin/bash
```
エラー情報がない場合は、ソフトリンクの修正に成功しています。
5.レスキューモードを終了して、システムを起動します。
