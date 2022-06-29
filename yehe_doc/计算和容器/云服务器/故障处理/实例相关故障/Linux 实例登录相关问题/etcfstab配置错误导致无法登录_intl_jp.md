## 故障について[](id:symptom)
CVMへのログインに失敗し、VNCでログインした後、「Welcome to emergency mode」というメッセージが表示され、システムの起動に失敗したことを確認します。以下の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


## 考えられる原因
`/etc/fstab`が適切に設定されていない恐れがあります。
例えば、`/etc/fstab`でデバイス名を使用してディスクを自動的にマウントするように設定したが、CVMの再起動時にデバイス名が変更されたため、システムが正常に起動できなくなります。


## ソリューション
[処理手順](#ProcessingSteps)を参照して`/etc/fstab`設定ファイルを修正し、サーバを再起動してから検証してください。


## 処理手順[](id:ProcessingSteps)

インスタンスに入りこの問題に対処するには、次の2つの方法があります。

<dx-tabs>
：：： 方法1：VNCを使用してログインします（推奨）[](id：useVNC)
- [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)。
2. VNC画面に入ったら、[故障について](#symptom)に表示されている画面が表示されたら、rootアカウントのパスワードを入力し、**Enter**キーを押してCVMにログインします。
 -入力したパスワードはデフォルトで表示されません。
 - rootアカウントのパスワードを持っていないか、それを忘れた場合は、方法2をご参照ください。
3. [](id:Step3)以下のコマンドを実行して、`/etc/fstab ファイル`をバックアップします。このドキュメントではディレクトリの配下にバックアップすることを例とします。
```shellsession
cp /etc/fstab /home
```
4. 以下のコマンドを実行して、VIエディタを利用して`/etc/fstab` ファイルを開きます。
```shellsession
vi /etc/fstab
```
5. **i**キーを押して編集モードに入り、カーソルを誤った設定の行の先頭に移動し、`#`と入力して行の設定をコメントします。以下の通りです。
<dx-alert infotype="explain" title="">
設定が間違っているかどうかと判断できない場合は、システムディスクを除くすべてのマウントディスクの設定にコメントを付け、CVMが正常に戻ってから[ステップ8](#Step7)を参照して設定することをお勧めします。
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1c238789186d7f24c0244e0307bc3a22.png"/>
6. [](id:Step6)**Esc**を押して、**:wq**を入力し、**Enter**を押してください。設定を保存して、エディターを終了します。
7. コンソールからインスタンスを再起動し、起動後に正常に起動してログインできるか確認します。
<dx-alert infotype="explain" title="">
コンソールでインスタンスを再起動する具体的な手順については[インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
</dx-alert>
8. [](id：Step8)ログインが成功した後、ディスクの自動マウントを設定する場合は、[/etc/fstabファイルの設定](https://intl.cloud.tencent.com/document/product/362/40001)を参照して設定してください。

:::
：：：方法2：レスキューモード[](id：useRescue)を使用します
1. [レスキューモードを使用]（https://intl.cloud.tencent.com/document/product/213/46157）を参照して、レスキューモードに入ります。
<dx-alert infotype="notice" title="">
「レスキューモードを使用したシステム修復」(https://intl.cloud.tencent.com/document/product/213/46157?lang=en&pg=#using-rescue-mode-to-repair-system)手順の`mount`と`chroot`に関連するコマンドを実行し、業務自体のシステムに入ったことを確認する必要があります。
</dx-alert>
2. 方法1のステップ3（#Step3）〜ステップ6（#Step6）に従って、`/etc/fstab`ファイルを修復します。
3. [レスキューモードを終了](https://intl.cloud.tencent.com/document/product/213/46157?lang=en&pg=#exiting-rescue-mode)を参照して、レスキューモードを終了します。
4. インスタンスがレスキューモードを終了すると、シャットダウン状態になります。[インスタンスの起動](https://intl.cloud.tencent.com/document/product/213/38168) を参考に起動し、起動後にシステムが正常に起動してログインできるか検証してください。
5. ログインが成功した後、ディスクの自動マウントを設定する場合は、[/etc/fstabファイルの設定](https://intl.cloud.tencent.com/document/product/362/40001)を参照して設定してください。

:::
</dx-tabs>







