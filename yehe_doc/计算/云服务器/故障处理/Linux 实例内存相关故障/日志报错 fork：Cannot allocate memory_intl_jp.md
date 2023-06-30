##故障について
ログに、「fork：Cannot allocate memory」というエラー情報が表示されます。下図のとおりです。
![](https://main.qcloudimg.com/raw/db85a43e7495f1655a2b59063ffc33e3.png)

## 考えられる原因
プロセス数の限度を超えたことが原因と考えられます。システム内部のプロセス総数が`pid_max`に達すると、新しいプロセスが作成されたときに「fork：Cannot allocate memory」というエラーが報告されます。

## ソリューション
1. [処理手順](#ProcessingSteps)を参照して、インスタンスのメモリ使用率が高すぎないかどうかを確認します。
2. 総プロセス数が限度を超えていないか確認し、プロセス総数`pid_max`の設定を変更します。 



## 処理手順[](id:ProcessingSteps)
1. [メモリ使用率が高すぎる問題の処理](https://intl.cloud.tencent.com/document/product/213/40501)を参照して、インスタンスのメモリ使用率が高すぎないかどうかを確認します。インスタンスのメモリ使用率が正常な場合は、次の手順に進みます。
2. 以下のコマンドを実行して、システムの`pid_max`値を確認します。
```
sysctl  -a | grep pid_max
```
返された結果に基づき、対応する操作を行います。
 - 返された結果が下図のとおりで、`pid_max`デフォルト値が32768である場合は、次の手順にお進みください。
![](https://main.qcloudimg.com/raw/816a0bd183244aadf14e04c6ed200d68.png)
 - 返されたエラー情報が「fork：Cannot allocate memory」である場合は、次のコマンドを実行し、`pid_max`を一時的に増やす必要があります。
```
echo 42768 > /proc/sys/kernel/pid_max
```
もう一度コマンドを実行し、システムの`pid_max`値を確認します。
3. 以下のコマンドを実行して、システム内部のプロセス総数を確認します。
```
pstree -p | wc -l
```
プロセス総数が`pid_max`に達すると、システムは新しいプロセスを作成するときに「fork：Cannot allocate memory」というエラーを報告します。
<dx-alert infotype="explain" title="">
`ps -efL`コマンドを実行して、プロセスの起動が多いプログラムを特定します。
</dx-alert>
4. `/etc/sysctl.conf`設定ファイルの`kernel.pid_max`値を65535に変更して、プロセスの数を増やします。変更が完了すると、下図のようになります。
![](https://main.qcloudimg.com/raw/a4bbf49b3236b9f50988e914298adb31.png)
5. 以下のコマンドを実行して、直ちに設定を有効にします。
```
sysctl -p
```
