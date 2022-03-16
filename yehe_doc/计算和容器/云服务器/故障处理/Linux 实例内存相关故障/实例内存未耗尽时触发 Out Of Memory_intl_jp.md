##故障について
Linux CVMは、メモリ使用率が100%でない場合、OOM(Out Of Memory)をトリガーします。下図のとおりです。
![](https://main.qcloudimg.com/raw/72cbd63ac445a1caa8d82fa1e55ba5a5.png)

## 考えられる原因
システムで使用可能なメモリが`min_free_kbytes`の値よりも低いことが原因と考えられます。`min_free_kbytes`の値は、Linuxシステムに最低限の空きメモリ(Kbytes)の予約を強制することを意味します。システムの使用可能なメモリが、設定した`min_free_kbytes`の値よりも低い場合、デフォルトでシステムがoom-killerを起動するか、強制的に再起動します。具体的な挙動は、カーネルパラメータ`vm.panic_on_oom`の値によって決定付けられます。
 - `vm.panic_on_oom=0`の場合、システムはOOMを提示し、oom-killerを起動して、メモリの占有が最も多いプロセスを強制終了します。
 - `vm.panic_on_oom =1`の場合、システムは自動的に再起動します。

## ソリューション
1. [処理手順](#ProcessingSteps)を参照して、トラブルシューティングを行います。インスタンスのメモリ使用率が高すぎないか、またプロセス総数が制限されていないか確認してください。
2. `min_free_kbytes`値の設定を確認し、正しい設定に変更します。


## 処理手順[](id:ProcessingSteps)
1. [メモリ使用率が高すぎる問題の処理](https://intl.cloud.tencent.com/document/product/213/40501)を参照して、インスタンスのメモリ使用率が高すぎないかどうかを確認します。インスタンスのメモリ使用率が正常な場合は、次の手順に進みます。
2. [ログエラーfork：Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40502)を参照して、プロセス数が限度を超えていないかどうか確認してください。プロセス総数が限度を超えていない場合は、次の手順に進んでください。
3. CVMにログインし、以下のコマンドを実行して、`min_free_kbytes`の値を確認します。
```
sysctl -a | grep min_free
```
`min_free_kbytes`の値の単位はkbytesです。下図に示すとおり、`min_free_kbytes = 1024000`は1GBを意味します。
![](https://main.qcloudimg.com/raw/18ac6c04962abfbf67132eab1a604167.png)
4. 以下のコマンドを実行して、VIMエディタを使用し`/etc/sysctl.conf`構成ファイルを開きます。
```
vim /etc/sysctl.conf
```
5. **i**を押して編集モードに入り、`vm.min_free_kbytes`設定項目を変更します。この設定項目が存在しない場合は、設定ファイルに直接追加すればOKです。
<dx-alert infotype="explain" title="">
`vm.min_free_kbytes`の値をメモリ合計の1%以下に変更することをお勧めします。
</dx-alert>
6. **Esc**を押して**:wq**と入力し、次に**Enter**を押してVIMエディタを保存して終了します。
7. 以下のコマンドを実行して、設定を有効にすれば完了です
```
sysctl -p
```
